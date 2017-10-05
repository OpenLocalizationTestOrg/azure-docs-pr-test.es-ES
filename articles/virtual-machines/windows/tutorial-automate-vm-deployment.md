---
title: "Personalizar una máquina virtual de Windows en Azure | Microsoft Docs"
description: "Obtenga información sobre cómo usar la extensión de script personalizado y Key Vault para personalizar las máquinas virtuales de Windows en Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 3be58bf8afbcff018b2b0d69a0e08c2c9ab1fca7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-customize-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="04290-103">Cómo personalizar una máquina virtual de Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="04290-103">How to customize a Windows virtual machine in Azure</span></span>
<span data-ttu-id="04290-104">Para configurar las máquinas virtuales de una manera rápida y coherente, normalmente se desea alguna forma de automatización.</span><span class="sxs-lookup"><span data-stu-id="04290-104">To configure virtual machines (VMs) in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="04290-105">Un enfoque común para personalizar una máquina virtual de Windows consiste en usar la [Extensión de la secuencia de comandos personalizada para Windows](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="04290-105">A common approach to customize a Windows VM is to use [Custom Script Extension for Windows](extensions-customscript.md).</span></span> <span data-ttu-id="04290-106">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="04290-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="04290-107">Usar la extensión de script personalizada para instalar IIS</span><span class="sxs-lookup"><span data-stu-id="04290-107">Use the Custom Script Extension to install IIS</span></span>
> * <span data-ttu-id="04290-108">Crear una máquina virtual que use la extensión de script personalizada</span><span class="sxs-lookup"><span data-stu-id="04290-108">Create a VM that uses the Custom Script Extension</span></span>
> * <span data-ttu-id="04290-109">Ver un sitio IIS en funcionamiento después de aplicar la extensión</span><span class="sxs-lookup"><span data-stu-id="04290-109">View a running IIS site after the extension is applied</span></span>

<span data-ttu-id="04290-110">Para realizar este tutorial es necesaria la versión 3.6 del módulo de Azure PowerShell, o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="04290-110">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="04290-111">Ejecute ` Get-Module -ListAvailable AzureRM` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="04290-111">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="04290-112">Si necesita actualizarla, consulte [Instalación del módulo de Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="04290-112">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="custom-script-extension-overview"></a><span data-ttu-id="04290-113">Información general de la extensión de script personalizado</span><span class="sxs-lookup"><span data-stu-id="04290-113">Custom script extension overview</span></span>
<span data-ttu-id="04290-114">La extensión de script personalizado descarga y ejecuta scripts en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="04290-114">The Custom Script Extension downloads and executes scripts on Azure VMs.</span></span> <span data-ttu-id="04290-115">Esta extensión es útil para la configuración posterior a la implementación, la instalación de software o cualquier otra tarea de configuración o administración.</span><span class="sxs-lookup"><span data-stu-id="04290-115">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="04290-116">Los scripts se pueden descargar desde Azure Storage o GitHub, o se pueden proporcionar a Azure Portal en el tiempo de ejecución de la extensión.</span><span class="sxs-lookup"><span data-stu-id="04290-116">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span></span>

<span data-ttu-id="04290-117">La extensión de script personalizado se integra con las plantillas de Azure Resource Manager y también se puede ejecutar mediante la CLI de Azure, PowerShell, Azure Portal o la API de REST de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="04290-117">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="04290-118">Se puede usar la extensión de script personalizado con máquinas virtuales de Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="04290-118">You can use the Custom Script Extension with both Windows and Linux VMs.</span></span>


## <a name="create-virtual-machine"></a><span data-ttu-id="04290-119">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="04290-119">Create virtual machine</span></span>
<span data-ttu-id="04290-120">Antes de poder crear una máquina virtual, cree un grupo de recursos con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="04290-120">Before you can create a VM, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="04290-121">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroupAutomate* en la ubicación *EastUS*:</span><span class="sxs-lookup"><span data-stu-id="04290-121">The following example creates a resource group named *myResourceGroupAutomate* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

<span data-ttu-id="04290-122">Establezca un nombre de usuario de administrador y una contraseña para las máquinas virtuales con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="04290-122">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="04290-123">Ahora puede crear la máquina virtual con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="04290-123">Now you can create the VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="04290-124">En el ejemplo siguiente se crean los componentes de red virtual necesarios, la configuración del sistema operativo y, después, se crea una máquina virtual denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="04290-124">The following example creates the required virtual network components, the OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName myResourceGroupAutomate -Location EastUS -VM $vmConfig
```

<span data-ttu-id="04290-125">Los recursos y la máquina virtual tardan unos minutos en crearse.</span><span class="sxs-lookup"><span data-stu-id="04290-125">It takes a few minutes for the resources and VM to be created.</span></span>


## <a name="automate-iis-install"></a><span data-ttu-id="04290-126">Automatizar la instalación de IIS</span><span class="sxs-lookup"><span data-stu-id="04290-126">Automate IIS install</span></span>
<span data-ttu-id="04290-127">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) para instalar la extensión de script personalizado.</span><span class="sxs-lookup"><span data-stu-id="04290-127">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to install the Custom Script Extension.</span></span> <span data-ttu-id="04290-128">La extensión ejecuta `powershell Add-WindowsFeature Web-Server` para instalar el servidor web de IIS y después actualiza la página *Default.htm* para mostrar el nombre de host de la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="04290-128">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver and then updates the *Default.htm* page to show the hostname of the VM:</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName myResourceGroupAutomate `
    -ExtensionName IIS `
    -VMName myVM `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
    -Location EastUS
```


## <a name="test-web-site"></a><span data-ttu-id="04290-129">Sitio web de prueba</span><span class="sxs-lookup"><span data-stu-id="04290-129">Test web site</span></span>
<span data-ttu-id="04290-130">Obtenga la dirección IP pública del equilibrador de carga con [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="04290-130">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="04290-131">En el ejemplo siguiente se obtiene la dirección IP de *myPublicIP* que se ha creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="04290-131">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

<span data-ttu-id="04290-132">A continuación, puede escribir la dirección IP pública en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="04290-132">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="04290-133">Se muestra el sitio web, incluido el nombre de host de la máquina virtual a la que el equilibrador de carga distribuye el tráfico como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="04290-133">The website is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![Ejecución del sitio web de IIS](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a><span data-ttu-id="04290-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="04290-135">Next steps</span></span>

<span data-ttu-id="04290-136">En este tutorial, automatizó la instalación IIS en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="04290-136">In this tutorial, you automated the IIS install on a VM.</span></span> <span data-ttu-id="04290-137">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="04290-137">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="04290-138">Usar la extensión de script personalizada para instalar IIS</span><span class="sxs-lookup"><span data-stu-id="04290-138">Use the Custom Script Extension to install IIS</span></span>
> * <span data-ttu-id="04290-139">Crear una máquina virtual que use la extensión de script personalizada</span><span class="sxs-lookup"><span data-stu-id="04290-139">Create a VM that uses the Custom Script Extension</span></span>
> * <span data-ttu-id="04290-140">Ver un sitio IIS en funcionamiento después de aplicar la extensión</span><span class="sxs-lookup"><span data-stu-id="04290-140">View a running IIS site after the extension is applied</span></span>

<span data-ttu-id="04290-141">Avanzar al siguiente tutorial para aprender a crear imágenes de máquina virtual personalizadas.</span><span class="sxs-lookup"><span data-stu-id="04290-141">Advance to the next tutorial to learn how to create custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="04290-142">Creación de imágenes personalizadas de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="04290-142">Create custom VM images</span></span>](./tutorial-custom-images.md)
