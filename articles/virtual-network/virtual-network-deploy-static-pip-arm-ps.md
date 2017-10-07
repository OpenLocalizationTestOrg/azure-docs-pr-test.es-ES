---
title: "aaaCreate una máquina virtual con una dirección pública estática de IP - PowerShell de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual con una dirección IP pública estática trata acerca del uso de PowerShell."
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
ms.openlocfilehash: 0d2b88319cb114b8616f60dbee41e8fdc6d8b1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-powershell"></a><span data-ttu-id="fc376-103">Creación de una máquina virtual con una dirección IP pública estática mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc376-103">Create a VM with a static public IP address using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fc376-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="fc376-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="fc376-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc376-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="fc376-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="fc376-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="fc376-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="fc376-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="fc376-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="fc376-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="fc376-109">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fc376-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fc376-110">Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar del modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc376-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="step-1---start-your-script"></a><span data-ttu-id="fc376-111">Paso 1: inicio del script</span><span class="sxs-lookup"><span data-stu-id="fc376-111">Step 1 - Start your script</span></span>
<span data-ttu-id="fc376-112">Puede descargar Hola script completo de PowerShell usa [aquí](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="fc376-112">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span></span> <span data-ttu-id="fc376-113">Siga los pasos de hello debajo toochange Hola script toowork en su entorno.</span><span class="sxs-lookup"><span data-stu-id="fc376-113">Follow hello steps below toochange hello script toowork in your environment.</span></span>

<span data-ttu-id="fc376-114">Cambiar los valores de hello de hello las variables siguientes basadas en valores de hello desea toouse para su implementación.</span><span class="sxs-lookup"><span data-stu-id="fc376-114">Change hello values of hello variables below based on hello values you want toouse for your deployment.</span></span> <span data-ttu-id="fc376-115">Hola siguiendo el escenario de toohello de asignación de valores usado en este artículo:</span><span class="sxs-lookup"><span data-stu-id="fc376-115">hello following values map toohello scenario used in this article:</span></span>

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

## <a name="step-2---create-hello-necessary-resources-for-your-vm"></a><span data-ttu-id="fc376-116">Paso 2: crear Hola recursos necesarios para la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fc376-116">Step 2 - Create hello necessary resources for your VM</span></span>
<span data-ttu-id="fc376-117">Antes de crear una máquina virtual, se necesita un grupo de recursos, red virtual, pública IP y NIC toobe usa Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fc376-117">Before creating a VM, you need a resource group, VNet, public IP, and NIC toobe used by hello VM.</span></span>

1. <span data-ttu-id="fc376-118">Cree un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="fc376-118">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $rgName -Location $location
    ```

2. <span data-ttu-id="fc376-119">Crear Hola red virtual y subred.</span><span class="sxs-lookup"><span data-stu-id="fc376-119">Create hello VNet and subnet.</span></span>

    ```powershell
    $vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName `
        -AddressPrefix $vnetPrefix -Location $location

    Add-AzureRmVirtualNetworkSubnetConfig -Name $subnetName `
        -VirtualNetwork $vnet -AddressPrefix $subnetPrefix

    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

3. <span data-ttu-id="fc376-120">Crear recurso IP público Hola.</span><span class="sxs-lookup"><span data-stu-id="fc376-120">Create hello public IP resource.</span></span> 

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name $pipName -ResourceGroupName $rgName `
        -AllocationMethod Static -DomainNameLabel $dnsName -Location $location
    ```

4. <span data-ttu-id="fc376-121">Crear la interfaz de red (NIC) de Hola para hello VM en la subred de hello creado anteriormente, con la dirección IP pública de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc376-121">Create hello network interface (NIC) for hello VM in hello subnet created above, with hello public IP.</span></span> <span data-ttu-id="fc376-122">Observe Hola primer cmdlet recuperar Hola red virtual de Azure, esto es necesario porque un `Set-AzureRmVirtualNetwork` se ha ejecutado toochange Hola red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="fc376-122">Notice hello first cmdlet retrieving hello VNet from Azure, this is necessary since a `Set-AzureRmVirtualNetwork` was executed toochange hello existing VNet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnetName
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
        -Subnet $subnet -Location $location -PrivateIpAddress $privateIPAddress `
        -PublicIpAddress $pip
    ```

5. <span data-ttu-id="fc376-123">Crear un hello toohost de cuenta de almacenamiento unidad de sistema operativo de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fc376-123">Create a storage account toohost hello VM OS drive.</span></span>

    ```powershell
    $stdStorageAccount = New-AzureRmStorageAccount -Name $stdStorageAccountName `
    -ResourceGroupName $rgName -Type Standard_LRS -Location $location
    ```

## <a name="step-3---create-hello-vm"></a><span data-ttu-id="fc376-124">Paso 3: crear Hola VM</span><span class="sxs-lookup"><span data-stu-id="fc376-124">Step 3 - Create hello VM</span></span>
<span data-ttu-id="fc376-125">Ahora que todos los recursos necesarios están en su lugar, puede crear una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fc376-125">Now that all necessary resources are in place, you can create a new VM.</span></span>

1. <span data-ttu-id="fc376-126">Crear objeto de configuración de Hola para hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fc376-126">Create hello configuration object for hello VM.</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
    ```

2. <span data-ttu-id="fc376-127">Obtiene las credenciales de cuenta de administrador local de VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc376-127">Get credentials for hello VM local administrator account.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

3. <span data-ttu-id="fc376-128">Cree un objeto de configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fc376-128">Create a VM configuration object.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    ```

4. <span data-ttu-id="fc376-129">Establece la imagen de sistema operativo de Hola de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fc376-129">Set hello operating system image for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher `
        -Offer $offer -Skus $sku -Version $version
    ```

5. <span data-ttu-id="fc376-130">Configurar el disco de SO Hola.</span><span class="sxs-lookup"><span data-stu-id="fc376-130">Configure hello OS disk.</span></span>

    ```powershell
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    ```

6. <span data-ttu-id="fc376-131">Agregar Hola NIC toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fc376-131">Add hello NIC toohello VM.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id -Primary
    ```

7. <span data-ttu-id="fc376-132">Crear Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fc376-132">Create hello VM.</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $rgName -Location $location
    ```

8. <span data-ttu-id="fc376-133">Guarde el archivo de script de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc376-133">Save hello script file.</span></span>

## <a name="step-4---run-hello-script"></a><span data-ttu-id="fc376-134">Paso 4: secuencia de comandos de ejecución Hola</span><span class="sxs-lookup"><span data-stu-id="fc376-134">Step 4 - Run hello script</span></span>
<span data-ttu-id="fc376-135">Después de realizar los cambios necesarios y descripción de script de Hola mostrar anteriormente, ejecutar script de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc376-135">After making any necessary changes, and understanding hello script show above, run hello script.</span></span> 

1. <span data-ttu-id="fc376-136">Desde una consola de PowerShell o ISE de PowerShell, ejecute el script de Hola anterior.</span><span class="sxs-lookup"><span data-stu-id="fc376-136">From a PowerShell console, or PowerShell ISE, run hello script above.</span></span>
2. <span data-ttu-id="fc376-137">Hola después de salida debe mostrarse después de unos minutos:</span><span class="sxs-lookup"><span data-stu-id="fc376-137">hello following output should be displayed after a few minutes:</span></span>
   
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

