---
title: "aaaAzure inicio rápido: crear VM de Windows PowerShell | Documentos de Microsoft"
description: "Aprender rápidamente toocreate una máquina virtual de Windows con PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5e92435bf7ee443a01c158fed91c356363e2f425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a><span data-ttu-id="7939d-103">Creación de una máquina virtual Windows con PowerShell</span><span class="sxs-lookup"><span data-stu-id="7939d-103">Create a Windows virtual machine with PowerShell</span></span>

<span data-ttu-id="7939d-104">módulo de PowerShell de Azure de Hello es toocreate usado y administrar recursos de Azure desde la línea de comandos de PowerShell de Hola o en scripts.</span><span class="sxs-lookup"><span data-stu-id="7939d-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="7939d-105">Esta guía se detalla mediante toocreate de PowerShell y ejecute Windows Server 2016 con máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="7939d-105">This guide details using PowerShell toocreate and Azure virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="7939d-106">Una vez completada la implementación, se conecte toohello servidor e instale IIS.</span><span class="sxs-lookup"><span data-stu-id="7939d-106">Once deployment is complete, we connect toohello server and install IIS.</span></span>  

<span data-ttu-id="7939d-107">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="7939d-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="7939d-108">Este inicio rápido requiere hello Azure PowerShell versión 3.6 o posterior del módulo.</span><span class="sxs-lookup"><span data-stu-id="7939d-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="7939d-109">Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="7939d-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="7939d-110">Si necesita tooinstall o una actualización, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="7939d-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="7939d-111">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="7939d-111">Log in tooAzure</span></span>

<span data-ttu-id="7939d-112">Inicie sesión en la suscripción de Azure con hello tooyour `Login-AzureRmAccount` comando y siga hello en pantalla instrucciones.</span><span class="sxs-lookup"><span data-stu-id="7939d-112">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="7939d-113">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="7939d-113">Create resource group</span></span>

<span data-ttu-id="7939d-114">Cree un grupo de recursos de Azure con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="7939d-114">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="7939d-115">Un grupo de recursos es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="7939d-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a><span data-ttu-id="7939d-116">Creación de los recursos de red principales</span><span class="sxs-lookup"><span data-stu-id="7939d-116">Create networking resources</span></span>

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a><span data-ttu-id="7939d-117">Cree una red virtual, una subred, una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="7939d-117">Create a virtual network, subnet, and a public IP address.</span></span> 
<span data-ttu-id="7939d-118">Estos recursos son la máquina virtual de tooprovide usado red conectividad toohello y conéctelo toohello internet.</span><span class="sxs-lookup"><span data-stu-id="7939d-118">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location EastUS `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location EastUS `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="7939d-119">Cree un grupo de seguridad de red y una regla de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="7939d-119">Create a network security group and a network security group rule.</span></span> 
<span data-ttu-id="7939d-120">grupo de seguridad de red de Hello protege la máquina virtual de hello mediante reglas entrantes y salientes.</span><span class="sxs-lookup"><span data-stu-id="7939d-120">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="7939d-121">En este caso, se crea una regla de entrada para el puerto 3389, que permite las conexiones entrantes al Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="7939d-121">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span> <span data-ttu-id="7939d-122">También queremos toocreate una regla de entrada para el puerto 80, lo que permite el tráfico web entrante.</span><span class="sxs-lookup"><span data-stu-id="7939d-122">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-hello-virtual-machine"></a><span data-ttu-id="7939d-123">Crear una tarjeta de red de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="7939d-123">Create a network card for hello virtual machine.</span></span> 
<span data-ttu-id="7939d-124">Crear una tarjeta de red con [AzureRmNetworkInterface New](/powershell/module/azurerm.network/new-azurermnetworkinterface) para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="7939d-124">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="7939d-125">tarjeta de red de Hello conecta subred de tooa de máquina virtual de hello, grupo de seguridad de red y dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="7939d-125">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="7939d-126">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="7939d-126">Create virtual machine</span></span>

<span data-ttu-id="7939d-127">Cree una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7939d-127">Create a virtual machine configuration.</span></span> <span data-ttu-id="7939d-128">Esta configuración incluye valores de hello que se usan al implementar la máquina virtual de hello como una configuración de imagen, el tamaño y la autenticación de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7939d-128">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span> <span data-ttu-id="7939d-129">Cuando se realiza este paso, se le solicitará las credenciales.</span><span class="sxs-lookup"><span data-stu-id="7939d-129">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="7939d-130">los valores de Hello que especifique se configuran como nombre de usuario de hello y una contraseña para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="7939d-130">hello values that you enter are configured as hello user name and password for hello virtual machine.</span></span>

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

<span data-ttu-id="7939d-131">Crear la máquina virtual Hola con [AzureRmVM nuevo](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="7939d-131">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="7939d-132">Conectar máquina toovirtual</span><span class="sxs-lookup"><span data-stu-id="7939d-132">Connect toovirtual machine</span></span>

<span data-ttu-id="7939d-133">Una vez finalizada la implementación de hello, cree una conexión a escritorio remota con la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="7939d-133">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="7939d-134">Hola de uso [AzureRmPublicIpAddress Get](/powershell/module/azurerm.network/get-azurermpublicipaddress) dirección tooreturn Hola IP pública de la máquina virtual de Hola de comandos.</span><span class="sxs-lookup"><span data-stu-id="7939d-134">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="7939d-135">Tome nota de esta dirección IP para que pueda conectarse tooit con la conectividad de web tootest de explorador en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="7939d-135">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="7939d-136">Siguiente Hola de uso del comando toocreate una sesión de escritorio remoto con la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="7939d-136">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="7939d-137">Reemplace la dirección IP de hello con hello *publicIPAddress* de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7939d-137">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="7939d-138">Cuando se le solicite, escriba credenciales de hello usadas al crear la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="7939d-138">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a><span data-ttu-id="7939d-139">Instalación de IIS mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="7939d-139">Install IIS via PowerShell</span></span>

<span data-ttu-id="7939d-140">Ahora que ha iniciado en toohello máquina virtual de Azure, puede usar una sola línea de PowerShell tooinstall IIS y permitir el tráfico de web de tooallow de regla de hello firewall local.</span><span class="sxs-lookup"><span data-stu-id="7939d-140">Now that you have logged in toohello Azure VM, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="7939d-141">Abra un símbolo del sistema de PowerShell y ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="7939d-141">Open a PowerShell prompt and run hello following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="7939d-142">Hola de vista Página de bienvenida de IIS</span><span class="sxs-lookup"><span data-stu-id="7939d-142">View hello IIS welcome page</span></span>

<span data-ttu-id="7939d-143">Con IIS instalado y el puerto 80 ahora abierta en la máquina virtual de hello Internet, puede usar un explorador web de la página de bienvenida de IIS de elección tooview Hola predeterminado.</span><span class="sxs-lookup"><span data-stu-id="7939d-143">With IIS installed and port 80 now open on your VM from hello Internet, you can use a web browser of your choice tooview hello default IIS welcome page.</span></span> <span data-ttu-id="7939d-144">Estar seguro de hello toouse *publicIpAddress* documentó anteriormente página predeterminada de toovisit Hola.</span><span class="sxs-lookup"><span data-stu-id="7939d-144">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![Sitio predeterminado de IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="7939d-146">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="7939d-146">Clean up resources</span></span>

<span data-ttu-id="7939d-147">Cuando ya no necesite, puede usar hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) comandos tooremove grupo de recursos de hello, VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="7939d-147">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="7939d-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7939d-148">Next steps</span></span>

<span data-ttu-id="7939d-149">En esta guía de inicio rápido, ha implementado una máquina virtual simple y una regla de grupo de seguridad de red, y ha instalado un servidor web.</span><span class="sxs-lookup"><span data-stu-id="7939d-149">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="7939d-150">toolearn más información acerca de máquinas virtuales de Azure, continuar con tutorial toohello para máquinas virtuales de Windows.</span><span class="sxs-lookup"><span data-stu-id="7939d-150">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7939d-151">Tutoriales de máquinas virtuales Windows de Azure</span><span class="sxs-lookup"><span data-stu-id="7939d-151">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
