---
title: aaaCustomize una VM de Windows en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola extensión de script personalizado y el almacén de claves toocustomize máquinas virtuales de Windows en Azure"
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
ms.openlocfilehash: c03b2bb6d70875134c63ea2fe4c2e2c1777c2188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="ded66-103">¿Cómo toocustomize una máquina virtual de Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="ded66-103">How toocustomize a Windows virtual machine in Azure</span></span>
<span data-ttu-id="ded66-104">Normalmente se desea tooconfigure máquinas virtuales (VMs) de una manera rápida y coherente, alguna forma de automatización.</span><span class="sxs-lookup"><span data-stu-id="ded66-104">tooconfigure virtual machines (VMs) in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="ded66-105">Un toocustomize enfoque común una VM de Windows es toouse [extensión para ventanas de Script personalizado](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="ded66-105">A common approach toocustomize a Windows VM is toouse [Custom Script Extension for Windows](extensions-customscript.md).</span></span> <span data-ttu-id="ded66-106">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="ded66-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ded66-107">Usar la extensión de Script personalizado de hello tooinstall IIS</span><span class="sxs-lookup"><span data-stu-id="ded66-107">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="ded66-108">Crear una máquina virtual que usa Hola extensión de Script personalizado</span><span class="sxs-lookup"><span data-stu-id="ded66-108">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="ded66-109">Ver un sitio IIS en ejecución después de que se aplica la extensión de Hola</span><span class="sxs-lookup"><span data-stu-id="ded66-109">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="ded66-110">Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo.</span><span class="sxs-lookup"><span data-stu-id="ded66-110">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="ded66-111">Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="ded66-111">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="ded66-112">Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="ded66-112">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="custom-script-extension-overview"></a><span data-ttu-id="ded66-113">Información general de la extensión de script personalizado</span><span class="sxs-lookup"><span data-stu-id="ded66-113">Custom script extension overview</span></span>
<span data-ttu-id="ded66-114">Extensión de Script personalizado de Hello descarga y ejecuta scripts en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="ded66-114">hello Custom Script Extension downloads and executes scripts on Azure VMs.</span></span> <span data-ttu-id="ded66-115">Esta extensión es útil para la configuración posterior a la implementación, la instalación de software o cualquier otra tarea de configuración o administración.</span><span class="sxs-lookup"><span data-stu-id="ded66-115">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="ded66-116">Las secuencias de comandos pueden descargarse desde el almacenamiento de Azure o GitHub, o proporcionarse toohello portal de Azure en tiempo de ejecución de extensión.</span><span class="sxs-lookup"><span data-stu-id="ded66-116">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span>

<span data-ttu-id="ded66-117">Hola extensión de Script personalizado se integra con plantillas de Azure Resource Manager y también se puede ejecutar mediante Hola CLI de Azure, PowerShell, portal de Azure u Hola API de REST de máquina Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="ded66-117">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="ded66-118">Puede usar Hola extensión de Script personalizado con máquinas virtuales de Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="ded66-118">You can use hello Custom Script Extension with both Windows and Linux VMs.</span></span>


## <a name="create-virtual-machine"></a><span data-ttu-id="ded66-119">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="ded66-119">Create virtual machine</span></span>
<span data-ttu-id="ded66-120">Antes de poder crear una máquina virtual, cree un grupo de recursos con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="ded66-120">Before you can create a VM, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="ded66-121">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupAutomate* en hello *EastUS* ubicación:</span><span class="sxs-lookup"><span data-stu-id="ded66-121">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

<span data-ttu-id="ded66-122">Establecer un administrador username y password para máquinas virtuales de hello con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="ded66-122">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="ded66-123">Ahora puede crear Hola VM con [AzureRmVM nuevo](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="ded66-123">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="ded66-124">Hello ejemplo siguiente crea componentes de red virtual Hola necesario, configuración de hello SO y, a continuación, crea una máquina virtual denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="ded66-124">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

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

<span data-ttu-id="ded66-125">Tarda unos minutos para los recursos de Hola y toobe de máquina virtual que creó.</span><span class="sxs-lookup"><span data-stu-id="ded66-125">It takes a few minutes for hello resources and VM toobe created.</span></span>


## <a name="automate-iis-install"></a><span data-ttu-id="ded66-126">Automatizar la instalación de IIS</span><span class="sxs-lookup"><span data-stu-id="ded66-126">Automate IIS install</span></span>
<span data-ttu-id="ded66-127">Use [AzureRmVMExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall Hola extensión de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="ded66-127">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="ded66-128">Hola se ejecuta la extensión `powershell Add-WindowsFeature Web-Server` tooinstall Hola actualizaciones hello servidor Web IIS y, a continuación, *Default.htm* página tooshow Hola hostname de hello VM:</span><span class="sxs-lookup"><span data-stu-id="ded66-128">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

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


## <a name="test-web-site"></a><span data-ttu-id="ded66-129">Sitio web de prueba</span><span class="sxs-lookup"><span data-stu-id="ded66-129">Test web site</span></span>
<span data-ttu-id="ded66-130">Obtener dirección IP pública de Hola de un equilibrador de carga con [AzureRmPublicIPAddress Get](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="ded66-130">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="ded66-131">Hello en el ejemplo siguiente se obtiene la dirección IP de Hola para *myPublicIP* creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="ded66-131">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

<span data-ttu-id="ded66-132">A continuación, puede escribir la dirección IP pública hello en el Explorador de web tooa.</span><span class="sxs-lookup"><span data-stu-id="ded66-132">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="ded66-133">se muestra el sitio Web de Hello, incluyendo hostname Hola de hello VM ese equilibrador de carga de hello distribuye tooas de tráfico en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="ded66-133">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Ejecución del sitio web de IIS](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a><span data-ttu-id="ded66-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ded66-135">Next steps</span></span>

<span data-ttu-id="ded66-136">En este tutorial, se automatizó Hola IIS se instala en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ded66-136">In this tutorial, you automated hello IIS install on a VM.</span></span> <span data-ttu-id="ded66-137">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="ded66-137">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ded66-138">Usar la extensión de Script personalizado de hello tooinstall IIS</span><span class="sxs-lookup"><span data-stu-id="ded66-138">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="ded66-139">Crear una máquina virtual que usa Hola extensión de Script personalizado</span><span class="sxs-lookup"><span data-stu-id="ded66-139">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="ded66-140">Ver un sitio IIS en ejecución después de que se aplica la extensión de Hola</span><span class="sxs-lookup"><span data-stu-id="ded66-140">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="ded66-141">Avanzar toohello siguiente tutorial toolearn cómo toocreate imágenes de máquina virtual personalizadas.</span><span class="sxs-lookup"><span data-stu-id="ded66-141">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ded66-142">Creación de imágenes personalizadas de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="ded66-142">Create custom VM images</span></span>](./tutorial-custom-images.md)
