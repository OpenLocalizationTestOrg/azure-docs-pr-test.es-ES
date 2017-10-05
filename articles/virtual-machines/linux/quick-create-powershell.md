---
title: "Inicio rápido de Azure: creación de máquinas virtuales con PowerShell | Microsoft Docs"
description: "Aprenda rápidamente a crear una máquina virtual Linux con PowerShell."
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
ms.openlocfilehash: adcf492d4c2d935c880167675a1ed97566156ec7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a><span data-ttu-id="80a99-103">Creación de una máquina virtual Linux con PowerShell</span><span class="sxs-lookup"><span data-stu-id="80a99-103">Create a Linux virtual machine with PowerShell</span></span>

<span data-ttu-id="80a99-104">El módulo de Azure PowerShell se usa para crear y administrar recursos de Azure desde la línea de comandos de PowerShell o en scripts.</span><span class="sxs-lookup"><span data-stu-id="80a99-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span></span> <span data-ttu-id="80a99-105">En esta guía se detalla cómo usar el módulo de Azure PowerShell para implementar máquinas virtuales en las que se ejecuta el servidor de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="80a99-105">This guide details using the Azure PowerShell module to deploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="80a99-106">Una vez implementado el servidor, se crea una conexión SSH y se instala un servidor web NGINX.</span><span class="sxs-lookup"><span data-stu-id="80a99-106">Once the server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="80a99-107">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="80a99-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="80a99-108">Para realizar este tutorial de inicio rápido se requiere la versión 3.6 o superior del módulo de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80a99-108">This quick start requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="80a99-109">Ejecute ` Get-Module -ListAvailable AzureRM` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="80a99-109">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="80a99-110">Si necesita instalarla o actualizarla, consulte [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps) (Instalación y configuración de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="80a99-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="80a99-111">Por último, se tiene que almacenar una clave SSH pública con el nombre *id_rsa.pub* en el directorio *.ssh* de su perfil de usuario de Windows.</span><span class="sxs-lookup"><span data-stu-id="80a99-111">Finally, a public SSH key with the name *id_rsa.pub* needs to be stored in the *.ssh* directory of your Windows user profile.</span></span> <span data-ttu-id="80a99-112">Si quiere obtener información detallada sobre cómo crear claves SSH para Azure, consulte [este artículo](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="80a99-112">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="80a99-113">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="80a99-113">Log in to Azure</span></span>

<span data-ttu-id="80a99-114">Inicie sesión en la suscripción de Azure con el comando `Login-AzureRmAccount` y siga las instrucciones de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="80a99-114">Log in to your Azure subscription with the `Login-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="80a99-115">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="80a99-115">Create resource group</span></span>

<span data-ttu-id="80a99-116">Cree un grupo de recursos de Azure con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="80a99-116">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="80a99-117">Un grupo de recursos es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="80a99-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a><span data-ttu-id="80a99-118">Creación de los recursos de red principales</span><span class="sxs-lookup"><span data-stu-id="80a99-118">Create networking resources</span></span>

<span data-ttu-id="80a99-119">Cree una red virtual, una subred, una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="80a99-119">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="80a99-120">Estos recursos se utilizan para proporcionar conectividad de red a la máquina virtual y conectarse a Internet.</span><span class="sxs-lookup"><span data-stu-id="80a99-120">These resources are used to provide network connectivity to the virtual machine and connect it to the internet.</span></span>

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

<span data-ttu-id="80a99-121">Cree un grupo de seguridad de red y una regla de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="80a99-121">Create a network security group and a network security group rule.</span></span> <span data-ttu-id="80a99-122">El grupo de seguridad de red protege la máquina virtual con reglas entrantes y salientes.</span><span class="sxs-lookup"><span data-stu-id="80a99-122">The network security group secures the virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="80a99-123">En este caso, se crea una regla de entrada para el puerto 22, que permite las conexiones entrantes SSH.</span><span class="sxs-lookup"><span data-stu-id="80a99-123">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span></span> <span data-ttu-id="80a99-124">También queremos crear una regla de entrada para el puerto 80, que permita el tráfico web entrante.</span><span class="sxs-lookup"><span data-stu-id="80a99-124">We also want to create an inbound rule for port 80, which allows incoming web traffic.</span></span>

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

<span data-ttu-id="80a99-125">Cree una tarjeta de red con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="80a99-125">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for the virtual machine.</span></span> <span data-ttu-id="80a99-126">Esta conecta la máquina virtual a una subred, un grupo de seguridad de red y una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="80a99-126">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="80a99-127">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="80a99-127">Create virtual machine</span></span>

<span data-ttu-id="80a99-128">Cree una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="80a99-128">Create a virtual machine configuration.</span></span> <span data-ttu-id="80a99-129">Esta configuración incluye los ajustes que se usan al implementar la máquina virtual como una imagen de máquina virtual, el tamaño y la configuración de autenticación.</span><span class="sxs-lookup"><span data-stu-id="80a99-129">This configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, and authentication configuration.</span></span>

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

<span data-ttu-id="80a99-130">Cree la máquina virtual con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="80a99-130">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-to-virtual-machine"></a><span data-ttu-id="80a99-131">Conexión a la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="80a99-131">Connect to virtual machine</span></span>

<span data-ttu-id="80a99-132">Una vez finalizada la implementación, cree una conexión SSH con la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="80a99-132">After the deployment has completed, create an SSH connection with the virtual machine.</span></span>

<span data-ttu-id="80a99-133">Use el comando [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) para devolver la dirección IP pública de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="80a99-133">Use the [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command to return the public IP address of the virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="80a99-134">En un sistema con SSH instalado, usa el comando siguiente para conectarse a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="80a99-134">From a system with SSH installed, used the following command to connect to the virtual machine.</span></span> <span data-ttu-id="80a99-135">Si trabaja en Windows, puede usar [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) para crear la conexión.</span><span class="sxs-lookup"><span data-stu-id="80a99-135">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used to create the connection.</span></span> 

```bash 
ssh <Public IP Address>
```

<span data-ttu-id="80a99-136">Cuando se le solicite, el nombre de usuario de inicio de sesión es *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="80a99-136">When prompted, the login user name is *azureuser*.</span></span> <span data-ttu-id="80a99-137">Si se ha escrito una frase de contraseña al crear las claves SSH, debe escribirla también.</span><span class="sxs-lookup"><span data-stu-id="80a99-137">If a passphrase was entered when creating SSH keys, you need to enter this as well.</span></span>


## <a name="install-nginx"></a><span data-ttu-id="80a99-138">Instalación de NGINX</span><span class="sxs-lookup"><span data-stu-id="80a99-138">Install NGINX</span></span>

<span data-ttu-id="80a99-139">Use el siguiente script de bash para actualizar los orígenes de paquetes e instalar el paquete NGINX más reciente.</span><span class="sxs-lookup"><span data-stu-id="80a99-139">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-ngix-welcome-page"></a><span data-ttu-id="80a99-140">Página principal de NGIX</span><span class="sxs-lookup"><span data-stu-id="80a99-140">View the NGIX welcome page</span></span>

<span data-ttu-id="80a99-141">Con NGINX instalado y el puerto 80 abierto en la máquina virtual desde Internet, puede usar el explorador web que elija para ver la página principal de NGINX.</span><span class="sxs-lookup"><span data-stu-id="80a99-141">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span></span> <span data-ttu-id="80a99-142">Asegúrese de utilizar la dirección IP pública que ha anotado antes para visitar la página predeterminada.</span><span class="sxs-lookup"><span data-stu-id="80a99-142">Be sure to use the public IP address you documented above to visit the default page.</span></span> 

![Sitio predeterminado de NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="80a99-144">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="80a99-144">Clean up resources</span></span>

<span data-ttu-id="80a99-145">Cuando ya no se necesiten, puede usar el comando [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="80a99-145">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="80a99-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="80a99-146">Next steps</span></span>

<span data-ttu-id="80a99-147">En esta guía de inicio rápido, ha implementado una máquina virtual simple y una regla de grupo de seguridad de red, y ha instalado un servidor web.</span><span class="sxs-lookup"><span data-stu-id="80a99-147">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="80a99-148">Para más información acerca de las máquinas virtuales de Azure, continúe con el tutorial de máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="80a99-148">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="80a99-149">Tutoriales de máquinas virtuales Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="80a99-149">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
