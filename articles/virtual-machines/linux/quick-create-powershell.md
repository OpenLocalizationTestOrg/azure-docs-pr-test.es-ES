---
title: "aaaAzure inicio rápido: crear VM de PowerShell | Documentos de Microsoft"
description: "Aprender rápidamente toocreate un máquinas virtuales de Linux con PowerShell"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: f05ea7fedafe4fda660dc6084ae57ebf9dced473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a><span data-ttu-id="1e569-103">Creación de una máquina virtual Linux con PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e569-103">Create a Linux virtual machine with PowerShell</span></span>

<span data-ttu-id="1e569-104">módulo de PowerShell de Azure de Hello es toocreate usado y administrar recursos de Azure desde la línea de comandos de PowerShell de Hola o en scripts.</span><span class="sxs-lookup"><span data-stu-id="1e569-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="1e569-105">Esta guía se detalla mediante toodeploy de módulo de PowerShell de Azure de hello en una máquina virtual con el servidor de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="1e569-105">This guide details using hello Azure PowerShell module toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="1e569-106">Una vez implementado el servidor de hello, se crea una conexión SSH y se instala un servidor Web NGINX.</span><span class="sxs-lookup"><span data-stu-id="1e569-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="1e569-107">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="1e569-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="1e569-108">Este inicio rápido requiere hello Azure PowerShell versión 3.6 o posterior del módulo.</span><span class="sxs-lookup"><span data-stu-id="1e569-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="1e569-109">Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e569-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="1e569-110">Si necesita tooinstall o una actualización, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="1e569-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="1e569-111">Por último, una clave SSH pública con el nombre de hello *id_rsa.pub* necesita toobe almacenado en hello *.ssh* directorio de su perfil de usuario de Windows.</span><span class="sxs-lookup"><span data-stu-id="1e569-111">Finally, a public SSH key with hello name *id_rsa.pub* needs toobe stored in hello *.ssh* directory of your Windows user profile.</span></span> <span data-ttu-id="1e569-112">Si quiere obtener información detallada sobre cómo crear claves SSH para Azure, consulte [este artículo](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1e569-112">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="1e569-113">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="1e569-113">Log in tooAzure</span></span>

<span data-ttu-id="1e569-114">Inicie sesión en la suscripción de Azure con hello tooyour `Login-AzureRmAccount` comando y siga hello en pantalla instrucciones.</span><span class="sxs-lookup"><span data-stu-id="1e569-114">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="1e569-115">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="1e569-115">Create resource group</span></span>

<span data-ttu-id="1e569-116">Cree un grupo de recursos de Azure con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="1e569-116">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="1e569-117">Un grupo de recursos es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e569-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a><span data-ttu-id="1e569-118">Creación de los recursos de red principales</span><span class="sxs-lookup"><span data-stu-id="1e569-118">Create networking resources</span></span>

<span data-ttu-id="1e569-119">Cree una red virtual, una subred, una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="1e569-119">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="1e569-120">Estos recursos son la máquina virtual de tooprovide usado red conectividad toohello y conéctelo toohello internet.</span><span class="sxs-lookup"><span data-stu-id="1e569-120">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location eastus `
-Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location eastus `
-AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

<span data-ttu-id="1e569-121">Cree un grupo de seguridad de red y una regla de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="1e569-121">Create a network security group and a network security group rule.</span></span> <span data-ttu-id="1e569-122">grupo de seguridad de red de Hello protege la máquina virtual de hello mediante reglas entrantes y salientes.</span><span class="sxs-lookup"><span data-stu-id="1e569-122">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="1e569-123">En este caso, se crea una regla de entrada para el puerto 22, que permite las conexiones entrantes SSH.</span><span class="sxs-lookup"><span data-stu-id="1e569-123">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span></span> <span data-ttu-id="1e569-124">También queremos toocreate una regla de entrada para el puerto 80, lo que permite el tráfico web entrante.</span><span class="sxs-lookup"><span data-stu-id="1e569-124">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleSSH  -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location eastus `
-Name myNetworkSecurityGroup -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

<span data-ttu-id="1e569-125">Crear una tarjeta de red con [AzureRmNetworkInterface New](/powershell/module/azurerm.network/new-azurermnetworkinterface) para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e569-125">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="1e569-126">tarjeta de red de Hello conecta subred de tooa de máquina virtual de hello, grupo de seguridad de red y dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="1e569-126">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="1e569-127">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="1e569-127">Create virtual machine</span></span>

<span data-ttu-id="1e569-128">Cree una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1e569-128">Create a virtual machine configuration.</span></span> <span data-ttu-id="1e569-129">Esta configuración incluye valores de hello que se usan al implementar la máquina virtual de hello como una configuración de imagen, el tamaño y la autenticación de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1e569-129">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span>

```powershell
# Define a credential object
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("azureuser", $securePassword)

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Linux -ComputerName myVM -Credential $cred -DisablePasswordAuthentication | `
Set-AzureRmVMSourceImage -PublisherName Canonical -Offer UbuntuServer -Skus 14.04.2-LTS -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmconfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"
```

<span data-ttu-id="1e569-130">Crear la máquina virtual Hola con [AzureRmVM nuevo](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="1e569-130">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="1e569-131">Conectar máquina toovirtual</span><span class="sxs-lookup"><span data-stu-id="1e569-131">Connect toovirtual machine</span></span>

<span data-ttu-id="1e569-132">Una vez finalizada la implementación de hello, cree una conexión SSH con la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e569-132">After hello deployment has completed, create an SSH connection with hello virtual machine.</span></span>

<span data-ttu-id="1e569-133">Hola de uso [AzureRmPublicIpAddress Get](/powershell/module/azurerm.network/get-azurermpublicipaddress) dirección tooreturn Hola IP pública de la máquina virtual de Hola de comandos.</span><span class="sxs-lookup"><span data-stu-id="1e569-133">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="1e569-134">Desde un sistema con SSH instalado siguiente Hola usado comando tooconnect toohello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1e569-134">From a system with SSH installed, used hello following command tooconnect toohello virtual machine.</span></span> <span data-ttu-id="1e569-135">Si trabaja en Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) puede ser usado toocreate Hola conexión.</span><span class="sxs-lookup"><span data-stu-id="1e569-135">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used toocreate hello connection.</span></span> 

```bash 
ssh <Public IP Address>
```

<span data-ttu-id="1e569-136">Cuando se le solicite, nombre de usuario de inicio de sesión de hello es *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="1e569-136">When prompted, hello login user name is *azureuser*.</span></span> <span data-ttu-id="1e569-137">Si se ha introducido una frase de contraseña al crear las claves de SSH, deberá tooenter este también.</span><span class="sxs-lookup"><span data-stu-id="1e569-137">If a passphrase was entered when creating SSH keys, you need tooenter this as well.</span></span>


## <a name="install-nginx"></a><span data-ttu-id="1e569-138">Instalación de NGINX</span><span class="sxs-lookup"><span data-stu-id="1e569-138">Install NGINX</span></span>

<span data-ttu-id="1e569-139">Hola a uso continuación bash orígenes de paquetes de secuencia de comandos tooupdate e instala paquete NGINX más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e569-139">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a><span data-ttu-id="1e569-140">Página de bienvenida de vista hello NGIX</span><span class="sxs-lookup"><span data-stu-id="1e569-140">View hello NGIX welcome page</span></span>

<span data-ttu-id="1e569-141">Con NGINX instalado y el puerto 80 ahora abierta en la máquina virtual de Internet - Hola puede usar un explorador web de su elección tooview hello NGINX página de bienvenida predeterminada.</span><span class="sxs-lookup"><span data-stu-id="1e569-141">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="1e569-142">Ser seguro toouse Hola dirección IP pública que documentó anteriormente página predeterminada de toovisit Hola.</span><span class="sxs-lookup"><span data-stu-id="1e569-142">Be sure toouse hello public IP address you documented above toovisit hello default page.</span></span> 

![Sitio predeterminado de NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="1e569-144">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="1e569-144">Clean up resources</span></span>

<span data-ttu-id="1e569-145">Cuando ya no necesite, puede usar hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) comandos tooremove grupo de recursos de hello, VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="1e569-145">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="1e569-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1e569-146">Next steps</span></span>

<span data-ttu-id="1e569-147">En esta guía de inicio rápido, ha implementado una máquina virtual simple y una regla de grupo de seguridad de red, y ha instalado un servidor web.</span><span class="sxs-lookup"><span data-stu-id="1e569-147">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="1e569-148">toolearn más información acerca de máquinas virtuales de Azure, continuar con tutorial toohello para máquinas virtuales de Linux.</span><span class="sxs-lookup"><span data-stu-id="1e569-148">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1e569-149">Tutoriales de máquinas virtuales Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="1e569-149">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
