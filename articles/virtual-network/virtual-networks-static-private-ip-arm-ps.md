---
title: "aaaConfigure de direcciones IP privadas para las máquinas virtuales - PowerShell de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo las direcciones IP privadas de tooconfigure para máquinas virtuales con PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: d5f18929-15e3-40a2-9ee3-8188bc248ed8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4a3eb67de583e08208fcab40de1c2a8a9b65618c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a><span data-ttu-id="c9e10-103">Configuración de direcciones IP privadas para una máquina virtual mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9e10-103">Configure private IP addresses for a virtual machine using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

<span data-ttu-id="c9e10-104">Azure cuenta con dos modelos de implementación: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="c9e10-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="c9e10-105">Microsoft recomienda crear recursos a través del modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9e10-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="c9e10-106">Obtenga más información sobre toolearn Hola diferencias entre Hola dos modelos, leer hello [modelos de implementación de Azure comprender](../azure-resource-manager/resource-manager-deployment-model.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="c9e10-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="c9e10-107">Este artículo trata el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9e10-107">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="c9e10-108">También puede [administrar dirección IP privada estática en el modelo de implementación clásica de hello](virtual-networks-static-private-ip-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c9e10-108">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="c9e10-109">ejemplo de Hola PowerShell comandos siguientes esperan un entorno simple ya creado se basa en escenario de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="c9e10-109">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="c9e10-110">Si desea toorun comandos de hello, que se muestran en este documento, en primer lugar crear entorno de prueba de Hola se describe en [crear una red virtual](virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c9e10-110">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-ps.md).</span></span>

## <a name="create-a-vm-with-a-static-private-ip-address"></a><span data-ttu-id="c9e10-111">Creación de una máquina virtual con una dirección IP privada estática</span><span class="sxs-lookup"><span data-stu-id="c9e10-111">Create a VM with a static private IP address</span></span>
<span data-ttu-id="c9e10-112">una máquina virtual denominada toocreate *DNS01* en hello *front-end* subred de una red virtual denominada *TestVNet* con una dirección IP estática privada de *192.168.1.101*, Siga los pasos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="c9e10-112">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="c9e10-113">Establecer variables para la cuenta de almacenamiento de hello, ubicación, grupo de recursos y toobe las credenciales que utiliza.</span><span class="sxs-lookup"><span data-stu-id="c9e10-113">Set variables for hello storage account, location, resource group, and credentials toobe used.</span></span> <span data-ttu-id="c9e10-114">Necesitará tooenter un nombre de usuario y una contraseña para hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c9e10-114">You will need tooenter a user name and password for hello VM.</span></span> <span data-ttu-id="c9e10-115">grupo de cuentas y recursos de almacenamiento de Hello ya debe existir.</span><span class="sxs-lookup"><span data-stu-id="c9e10-115">hello storage account and resource group must already exist.</span></span>

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type hello name and password of hello local administrator account."
    ```

2. <span data-ttu-id="c9e10-116">Red virtual de recuperación Hola y de las subredes que desee toocreate Hola VM en.</span><span class="sxs-lookup"><span data-stu-id="c9e10-116">Retrieve hello virtual network and subnet you want toocreate hello VM in.</span></span>

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. <span data-ttu-id="c9e10-117">Si es necesario, cree un Hola de tooaccess VM pública para la dirección IP de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="c9e10-117">If necessary, create a public IP address tooaccess hello VM from hello Internet.</span></span>

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. <span data-ttu-id="c9e10-118">Cree una NIC con hello privada dirección IP estática que desea tooassign toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c9e10-118">Create a NIC using hello static private IP address you want tooassign toohello VM.</span></span> <span data-ttu-id="c9e10-119">Asegúrese de IP de hello seguro es Hola intervalo de subred que va a agregar Hola VM a.</span><span class="sxs-lookup"><span data-stu-id="c9e10-119">Make sure hello IP is from hello subnet range you are adding hello VM to.</span></span> <span data-ttu-id="c9e10-120">Se trata de hello paso principal de este artículo, donde se establece Hola privada toobe IP estática.</span><span class="sxs-lookup"><span data-stu-id="c9e10-120">This is hello main step for this article, where you set hello private IP toobe static.</span></span>

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. <span data-ttu-id="c9e10-121">Crear Hola máquina virtual con hello NIC creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c9e10-121">Create hello VM using hello NIC created above.</span></span>

    ```powershell
    $vm = New-AzureRmVMConfig -VMName DNS01 -VMSize "Standard_A1"
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName DNS01 `
    -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri = $storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/WindowsVMosDisk.vhd"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name "windowsvmosdisk" -VhdUri $osDiskUri `
    -CreateOption fromImage
    New-AzureRmVM -ResourceGroupName $rgName -Location $locName -VM $vm 
    ```

    <span data-ttu-id="c9e10-122">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="c9e10-122">Expected output:</span></span>
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a><span data-ttu-id="c9e10-123">Recuperación de la información de la dirección IP privada estática para una interfaz de red</span><span class="sxs-lookup"><span data-stu-id="c9e10-123">Retrieve static private IP address information for a network interface</span></span>
<span data-ttu-id="c9e10-124">información de hello máquinas virtuales crean con script de Hola anterior, ejecute el siguiente comando de PowerShell de Hola de direcciones IP privada estática de tooview hello y observar los valores de hello para *PrivateIpAddress* y  *PrivateIpAllocationMethod*:</span><span class="sxs-lookup"><span data-stu-id="c9e10-124">tooview hello static private IP address information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *PrivateIpAddress* and *PrivateIpAllocationMethod*:</span></span>

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

<span data-ttu-id="c9e10-125">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="c9e10-125">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Static",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a><span data-ttu-id="c9e10-126">Eliminación de una dirección IP privada estática desde una interfaz de red</span><span class="sxs-lookup"><span data-stu-id="c9e10-126">Remove a static private IP address from a network interface</span></span>
<span data-ttu-id="c9e10-127">tooremove Hola privada dirección IP estática agregado toohello VM en script de Hola anteriormente, ejecución Hola siga los comandos de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c9e10-127">tooremove hello static private IP address added toohello VM in hello script above, run hello following PowerShell commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="c9e10-128">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="c9e10-128">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WindowsVM"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Dynamic",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="add-a-static-private-ip-address-tooa-network-interface"></a><span data-ttu-id="c9e10-129">Agregue una estático privado IP dirección tooa interfaz de red</span><span class="sxs-lookup"><span data-stu-id="c9e10-129">Add a static private IP address tooa network interface</span></span>
<span data-ttu-id="c9e10-130">tooadd una toohello de dirección IP privada estática máquinas virtuales creadas con script de Hola anterior, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="c9e10-130">tooadd a static private IP address toohello VM created using hello script above, run hello following commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-hello-allocation-method-for-a-private-ip-address-assigned-tooa-network-interface"></a><span data-ttu-id="c9e10-131">Cambiar el método de asignación de Hola para una dirección IP privada asignada tooa interfaz de red</span><span class="sxs-lookup"><span data-stu-id="c9e10-131">Change hello allocation method for a private IP address assigned tooa network interface</span></span>

<span data-ttu-id="c9e10-132">Se asigna a una dirección IP privada tooa NIC con el método de asignación estática o dinámica de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9e10-132">A private IP address is assigned tooa NIC with hello static or dynamic allocation method.</span></span> <span data-ttu-id="c9e10-133">Después de iniciar una máquina virtual que había antes en hello detenido estado (desasignada), pueden cambiar las direcciones IP dinámicas.</span><span class="sxs-lookup"><span data-stu-id="c9e10-133">Dynamic IP addresses can change after starting a VM that was previously in hello stopped (deallocated) state.</span></span> <span data-ttu-id="c9e10-134">Potencialmente, esto puede causar problemas si hospeda un servicio que requiera Hola Hola VM misma dirección IP, incluso después de se reinicia desde un estado detenido (desasignado).</span><span class="sxs-lookup"><span data-stu-id="c9e10-134">This can potentially cause issues if hello VM is hosting a service that requires hello same IP address, even after restarts from a stopped (deallocated) state.</span></span> <span data-ttu-id="c9e10-135">Direcciones IP estáticas se conservan hasta que se elimine Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c9e10-135">Static IP addresses are retained until hello VM is deleted.</span></span> <span data-ttu-id="c9e10-136">método de asignación de hello toochange de una dirección IP, ejecute hello siguiente secuencia de comandos, que cambia el método de asignación de Hola de toostatic dinámica.</span><span class="sxs-lookup"><span data-stu-id="c9e10-136">toochange hello allocation method of an IP address, run hello following script, which changes hello allocation method from dynamic toostatic.</span></span> <span data-ttu-id="c9e10-137">Si el método de asignación de hello para la dirección IP privada actual hello es estático, cambiar *estático* demasiado*dinámica* antes de ejecutar el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9e10-137">If hello allocation method for hello current private IP address is static, change *Static* too*Dynamic* before executing hello script.</span></span>

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "hello allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for hello IP address" $IP"." -NoNewline
```

<span data-ttu-id="c9e10-138">Si no conoce el nombre de Hola de hello NIC, puede ver una lista de las NICs dentro de un grupo de recursos escribiendo el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="c9e10-138">If you don't know hello name of hello NIC, you can view a list of NICs within a resource group by entering hello following command:</span></span>

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a><span data-ttu-id="c9e10-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c9e10-139">Next steps</span></span>
* <span data-ttu-id="c9e10-140">Obtenga más información acerca de las [direcciones IP públicas reservadas](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="c9e10-140">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="c9e10-141">Obtenga información sobre las [direcciones IP públicas a nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="c9e10-141">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="c9e10-142">Consulte hello [API de REST para IP reservadas](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9e10-142">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

