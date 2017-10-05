---
title: "Creación de una máquina virtual con una dirección IP pública estática (Azure PowerShell) | Microsoft Docs"
description: "Obtenga información sobre cómo crear una máquina virtual con una dirección IP pública estática mediante PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ad975ab9-d69f-45c1-9e45-0d3f0f51e87e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e4c413d3cb5c242a16f3e534dafe322785a35141
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-powershell"></a><span data-ttu-id="d0c06-103">Creación de una máquina virtual con una dirección IP pública estática mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0c06-103">Create a VM with a static public IP address using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d0c06-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d0c06-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="d0c06-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0c06-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="d0c06-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d0c06-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="d0c06-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="d0c06-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="d0c06-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="d0c06-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="d0c06-109">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d0c06-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d0c06-110">En este artículo se describe el uso del modelo de implementación de Resource Manager, recomendado por Microsoft para la mayoría de las nuevas implementaciones en lugar del modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="d0c06-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="step-1---start-your-script"></a><span data-ttu-id="d0c06-111">Paso 1: inicio del script</span><span class="sxs-lookup"><span data-stu-id="d0c06-111">Step 1 - Start your script</span></span>
<span data-ttu-id="d0c06-112">Puede descargar el script de PowerShell completo que ha usado [aquí](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="d0c06-112">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span></span> <span data-ttu-id="d0c06-113">Siga los pasos siguientes para cambiar el script para que funcione en su entorno.</span><span class="sxs-lookup"><span data-stu-id="d0c06-113">Follow the steps below to change the script to work in your environment.</span></span>

<span data-ttu-id="d0c06-114">Cambie los valores de las variables siguientes según los valores que desee usar para la implementación.</span><span class="sxs-lookup"><span data-stu-id="d0c06-114">Change the values of the variables below based on the values you want to use for your deployment.</span></span> <span data-ttu-id="d0c06-115">Los valores siguientes se asignan al escenario usado en este artículo:</span><span class="sxs-lookup"><span data-stu-id="d0c06-115">The following values map to the scenario used in this article:</span></span>

```powershell
# Set variables resource group
$rgName                = "IaaSStory"
$location              = "West US"

# Set variables for VNet
$vnetName              = "WTestVNet"
$vnetPrefix            = "192.168.0.0/16"
$subnetName            = "FrontEnd"
$subnetPrefix          = "192.168.1.0/24"

# Set variables for storage
$stdStorageAccountName = "iaasstorystorage"

# Set variables for VM
$vmSize                = "Standard_A1"
$diskSize              = 127
$publisher             = "MicrosoftWindowsServer"
$offer                 = "WindowsServer"
$sku                   = "2012-R2-Datacenter"
$version               = "latest"
$vmName                = "WEB1"
$osDiskName            = "osdisk"
$nicName               = "NICWEB1"
$privateIPAddress      = "192.168.1.101"
$pipName               = "PIPWEB1"
$dnsName               = "iaasstoryws1"
```

## <a name="step-2---create-the-necessary-resources-for-your-vm"></a><span data-ttu-id="d0c06-116">Paso 2: creación de los recursos necesarios para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="d0c06-116">Step 2 - Create the necessary resources for your VM</span></span>
<span data-ttu-id="d0c06-117">Antes de crear una máquina virtual, necesitará un grupo de recursos, red virtual, dirección IP pública y NIC que se usará con la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d0c06-117">Before creating a VM, you need a resource group, VNet, public IP, and NIC to be used by the VM.</span></span>

1. <span data-ttu-id="d0c06-118">Cree un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d0c06-118">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $rgName -Location $location
    ```

2. <span data-ttu-id="d0c06-119">Cree la red virtual y subred.</span><span class="sxs-lookup"><span data-stu-id="d0c06-119">Create the VNet and subnet.</span></span>

    ```powershell
    $vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName `
        -AddressPrefix $vnetPrefix -Location $location

    Add-AzureRmVirtualNetworkSubnetConfig -Name $subnetName `
        -VirtualNetwork $vnet -AddressPrefix $subnetPrefix

    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

3. <span data-ttu-id="d0c06-120">Cree el recurso de IP pública.</span><span class="sxs-lookup"><span data-stu-id="d0c06-120">Create the public IP resource.</span></span> 

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name $pipName -ResourceGroupName $rgName `
        -AllocationMethod Static -DomainNameLabel $dnsName -Location $location
    ```

4. <span data-ttu-id="d0c06-121">Cree la interfaz de red (NIC) para la máquina virtual en la subred creada anteriormente, con la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="d0c06-121">Create the network interface (NIC) for the VM in the subnet created above, with the public IP.</span></span> <span data-ttu-id="d0c06-122">Observe el primer cmdlet que recupera la red virtual de Azure; esto es necesario porque se ejecutó `Set-AzureRmVirtualNetwork` para cambiar la red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="d0c06-122">Notice the first cmdlet retrieving the VNet from Azure, this is necessary since a `Set-AzureRmVirtualNetwork` was executed to change the existing VNet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnetName
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
        -Subnet $subnet -Location $location -PrivateIpAddress $privateIPAddress `
        -PublicIpAddress $pip
    ```

5. <span data-ttu-id="d0c06-123">Cree una cuenta de almacenamiento para hospedar la unidad del sistema operativo de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d0c06-123">Create a storage account to host the VM OS drive.</span></span>

    ```powershell
    $stdStorageAccount = New-AzureRmStorageAccount -Name $stdStorageAccountName `
    -ResourceGroupName $rgName -Type Standard_LRS -Location $location
    ```

## <a name="step-3---create-the-vm"></a><span data-ttu-id="d0c06-124">Paso 3: creación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d0c06-124">Step 3 - Create the VM</span></span>
<span data-ttu-id="d0c06-125">Ahora que todos los recursos necesarios están en su lugar, puede crear una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d0c06-125">Now that all necessary resources are in place, you can create a new VM.</span></span>

1. <span data-ttu-id="d0c06-126">Cree el objeto de configuración de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d0c06-126">Create the configuration object for the VM.</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
    ```

2. <span data-ttu-id="d0c06-127">Obtenga las credenciales para la cuenta de administrador local de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d0c06-127">Get credentials for the VM local administrator account.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type the name and password for the local administrator account."
    ```

3. <span data-ttu-id="d0c06-128">Cree un objeto de configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d0c06-128">Create a VM configuration object.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    ```

4. <span data-ttu-id="d0c06-129">Establezca la imagen de sistema operativo para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d0c06-129">Set the operating system image for the VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher `
        -Offer $offer -Skus $sku -Version $version
    ```

5. <span data-ttu-id="d0c06-130">Configure el disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="d0c06-130">Configure the OS disk.</span></span>

    ```powershell
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    ```

6. <span data-ttu-id="d0c06-131">Agregue la NIC a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d0c06-131">Add the NIC to the VM.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id -Primary
    ```

7. <span data-ttu-id="d0c06-132">Cree la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d0c06-132">Create the VM.</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $rgName -Location $location
    ```

8. <span data-ttu-id="d0c06-133">Guarde el archivo de script.</span><span class="sxs-lookup"><span data-stu-id="d0c06-133">Save the script file.</span></span>

## <a name="step-4---run-the-script"></a><span data-ttu-id="d0c06-134">Paso 4: ejecución del script</span><span class="sxs-lookup"><span data-stu-id="d0c06-134">Step 4 - Run the script</span></span>
<span data-ttu-id="d0c06-135">Después de realizar los cambios necesarios y comprender el script anterior, ejecute el script.</span><span class="sxs-lookup"><span data-stu-id="d0c06-135">After making any necessary changes, and understanding the script show above, run the script.</span></span> 

1. <span data-ttu-id="d0c06-136">Desde una consola de PowerShell o PowerShell ISE, ejecute el script anterior.</span><span class="sxs-lookup"><span data-stu-id="d0c06-136">From a PowerShell console, or PowerShell ISE, run the script above.</span></span>
2. <span data-ttu-id="d0c06-137">Después de unos minutos, se debería mostrar la salida siguiente:</span><span class="sxs-lookup"><span data-stu-id="d0c06-137">The following output should be displayed after a few minutes:</span></span>
   
        ResourceGroupName : IaaSStory
        Location          : westus
        ProvisioningState : Succeeded
        Tags              : 
        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory
   
        AddressSpace      : Microsoft.Azure.Commands.Network.Models.PSAddressSpace
        DhcpOptions       : Microsoft.Azure.Commands.Network.Models.PSDhcpOptions
        Subnets           : {FrontEnd}
        ProvisioningState : Succeeded
        AddressSpaceText  : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptionsText   : {}
        SubnetsText       : [
                              {
                                "Name": "FrontEnd",
                                "AddressPrefix": "192.168.1.0/24"
                              }
                            ]
        ResourceGroupName : IaaSStory
        Location          : westus
        ResourceGuid      : [Id]
        Tag               : {}
        TagsTable         : 
        Name              : WTestVNet
        Etag              : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        Id                : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet
   
        AddressSpace      : Microsoft.Azure.Commands.Network.Models.PSAddressSpace
        DhcpOptions       : Microsoft.Azure.Commands.Network.Models.PSDhcpOptions
        Subnets           : {FrontEnd}
        ProvisioningState : Succeeded
        AddressSpaceText  : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptionsText   : {
                              "DnsServers": []
                            }
        SubnetsText       : [
                              {
                                "Name": "FrontEnd",
                                "Etag": [Id],
                                "Id": "/subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "ProvisioningState": "Succeeded"
                              }
                            ]
        ResourceGroupName : IaaSStory
        Location          : westus
        ResourceGuid      : [Id]
        Tag               : {}
        TagsTable         : 
        Name              : WTestVNet
        Etag              : [Id]
        Id                : /subscriptions/[Subscription Id]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet
   
        TrackingOperationId : [Id]
        RequestId           : [Id]
        Status              : Succeeded
        StatusCode          : OK
        Output              : 
        StartTime           : [Subscription Id]
        EndTime             : [Subscription Id]
        Error               : 
        ErrorText           : 

