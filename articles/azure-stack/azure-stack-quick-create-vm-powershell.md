---
title: "aaaCreate una máquina virtual de Windows mediante el uso de PowerShell en la pila de Azure | Documentos de Microsoft"
description: "Cree una máquina virtual Windows con PowerShell en Azure Stack."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: de063eae6f0782d8916da991f285a9de6b41def4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-by-using-powershell-in-azure-stack"></a><span data-ttu-id="998c8-103">Creación de una máquina virtual Windows con PowerShell en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="998c8-103">Create a Windows virtual machine by using PowerShell in Azure Stack</span></span>

<span data-ttu-id="998c8-104">Máquinas virtuales en asigne de pila de Azure Hola flexibilidad de virtualización sin necesidad de toobuy y mantener Hola hardware físico que lo ejecuta.</span><span class="sxs-lookup"><span data-stu-id="998c8-104">Virtual machines in Azure Stack give you hello flexibility of virtualization without having toobuy and maintain hello physical hardware that runs it.</span></span> <span data-ttu-id="998c8-105">Cuando se usa máquinas virtuales, saber que hay algunas diferencias entre las características de Hola que están disponibles en Azure y pila de Azure, consulte toohello [consideraciones para las máquinas virtuales en Azure pila](azure-stack-vm-considerations.md) toolearn tema sobre Estas diferencias.</span><span class="sxs-lookup"><span data-stu-id="998c8-105">When you use Virtual Machines, understand that there are some differences between hello features that are available in Azure and Azure Stack, refer toohello [Considerations for virtual machines in Azure Stack](azure-stack-vm-considerations.md) topic toolearn about these differences.</span></span> 

<span data-ttu-id="998c8-106">Esta guía de detalles mediante PowerShell toocreate una máquina virtual de Windows Server 2016 en pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="998c8-106">This guide details using PowerShell toocreate a Windows Server 2016 virtual machine in Azure Stack.</span></span> <span data-ttu-id="998c8-107">Puede ejecutar pasos de hello descritos en este artículo desde Hola Kit de desarrollo de pila de Azure, o desde un cliente externo basado en Windows, si está conectado a través de VPN.</span><span class="sxs-lookup"><span data-stu-id="998c8-107">You can run hello steps described in this article either from hello Azure Stack Development Kit, or from a Windows-based external client if you are connected through VPN.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="998c8-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="998c8-108">Prerequisites</span></span>

1. <span data-ttu-id="998c8-109">marketplace de pila de Azure de Hello no contiene imágenes de Windows Server 2016 Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="998c8-109">hello Azure Stack marketplace doesn't contain hello Windows Server 2016 image by default.</span></span> <span data-ttu-id="998c8-110">Por lo tanto, para poder crear una máquina virtual, asegúrese de que el operador de pila de Azure hello [agrega marketplace de pila de Azure de hello Windows Server 2016 imagen toohello](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="998c8-110">So, before you can create a virtual machine, make sure that hello Azure Stack operator [adds hello Windows Server 2016 image toohello Azure Stack marketplace](azure-stack-add-default-image.md).</span></span> 
2. <span data-ttu-id="998c8-111">Pila de Azure requiere una versión específica de toocreate de módulo de PowerShell de Azure y administre recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="998c8-111">Azure Stack requires specific version of Azure PowerShell module toocreate and manage hello resources.</span></span> <span data-ttu-id="998c8-112">Siga los pasos de hello descritos en [instale PowerShell para Azure pila](azure-stack-powershell-install.md) versión requerida de tema tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="998c8-112">Use hello steps described in [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) topic tooinstall hello required version.</span></span>
3. [<span data-ttu-id="998c8-113">Configurar el entorno de PowerShell del usuario de hello pila de Azure</span><span class="sxs-lookup"><span data-stu-id="998c8-113">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md) 

## <a name="create-a-resource-group"></a><span data-ttu-id="998c8-114">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="998c8-114">Create a resource group</span></span>

<span data-ttu-id="998c8-115">Un grupo de recursos es un contenedor lógico en el que se implementan y se administran los recursos de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="998c8-115">A resource group is a logical container into which Azure Stack resources are deployed and managed.</span></span> <span data-ttu-id="998c8-116">Usar hello siguiente bloque de código toocreate un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="998c8-116">Use hello following code block toocreate a resource group.</span></span> <span data-ttu-id="998c8-117">Hemos asignado los valores para todas las variables en este documento, puede usarlas tal cual o asignar un valor diferente.</span><span class="sxs-lookup"><span data-stu-id="998c8-117">We have assigned values for all variables in this document, you can use them as is or assign a different value.</span></span>  

```powershell
# Create variables toostore hello location and resource group names.
$location = "local"
$ResourceGroupName = "myResourceGroup"

New-AzureRmResourceGroup `
  -Name $ResourceGroupName `
  -Location $location
```

## <a name="create-storage-resources"></a><span data-ttu-id="998c8-118">Creación de recursos de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="998c8-118">Create storage resources</span></span> 

<span data-ttu-id="998c8-119">Crear una cuenta de almacenamiento y una imagen de Windows Server 2016 hello toostore del contenedor de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="998c8-119">Create a storage account, and a storage container toostore hello Windows Server 2016 image.</span></span>

```powershell
# Create variables toostore hello storage account name and hello storage account SKU information
$StorageAccountName = "mystorageaccount"
$SkuName = "Standard_LRS"

# Create a new storage account
$StorageAccount = New-AzureRMStorageAccount `
  -Location $location `
  -ResourceGroupName $ResourceGroupName `
  -Type $SkuName `
  -Name $StorageAccountName

Set-AzureRmCurrentStorageAccount `
  -StorageAccountName $storageAccountName `
  -ResourceGroupName $resourceGroupName

# Create a storage container toostore hello virtual machine image
$containerName = 'osdisks'
$container = New-AzureStorageContainer `
  -Name $containerName `
  -Permission Blob
```

## <a name="create-networking-resources"></a><span data-ttu-id="998c8-120">Creación de los recursos de red principales</span><span class="sxs-lookup"><span data-stu-id="998c8-120">Create networking resources</span></span>

<span data-ttu-id="998c8-121">Cree una red virtual, una subred, una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="998c8-121">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="998c8-122">Estos recursos son utilizados tooprovide red conectividad toohello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="998c8-122">These resources are used tooprovide network connectivity toohello virtual machine.</span></span>  

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name MyVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -AllocationMethod Static `
  -IdleTimeoutInMinutes 4 `
  -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="998c8-123">Creación de un grupo de seguridad de red y una regla de grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="998c8-123">Create a network security group and a network security group rule</span></span>

<span data-ttu-id="998c8-124">grupo de seguridad de red de Hola protege máquinas virtuales de hello mediante reglas entrantes y salientes.</span><span class="sxs-lookup"><span data-stu-id="998c8-124">hello network security group secures hello virtual machine by using inbound and outbound rules.</span></span> <span data-ttu-id="998c8-125">Permite crear una regla de entrada para el puerto 3389 tooallow entrantes conexiones de escritorio remoto y una regla de entrada para el tráfico web tooallow entrante el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="998c8-125">Lets create an inbound rule for port 3389 tooallow incoming Remote Desktop connections and an inbound rule for port 80 tooallow incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRuleRDP `
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
  -Name myNetworkSecurityGroupRuleWWW `
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
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRuleRDP,$nsgRuleWeb 
```
 
### <a name="create-a-network-card-for-hello-virtual-machine"></a><span data-ttu-id="998c8-126">Crear una tarjeta de red de máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="998c8-126">Create a network card for hello virtual machine</span></span>

<span data-ttu-id="998c8-127">tarjeta de red de Hello conecta subred de tooa de máquina virtual de hello, grupo de seguridad de red y dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="998c8-127">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate it with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
  -Name myNic `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id `
  -NetworkSecurityGroupId $nsg.Id 
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="998c8-128">de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="998c8-128">Create a virtual machine</span></span>

<span data-ttu-id="998c8-129">Cree una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="998c8-129">Create a virtual machine configuration.</span></span> <span data-ttu-id="998c8-130">Hola incluye configuración de Hola que se usa al implementar la máquina virtual de hello como una imagen de máquina virtual, el tamaño, las credenciales.</span><span class="sxs-lookup"><span data-stu-id="998c8-130">hello configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, credentials.</span></span>

```powershell
# Define a credential object toostore hello username and password for hello virtual machine
$UserName='demouser'
$Password='Password@123'| ConvertTo-SecureString -Force -AsPlainText
$Credential=New-Object PSCredential($UserName,$Password)

# Create hello virtual machine configuration object
$VmName = "VirtualMachinelatest"
$VmSize = "Standard_A1"
$VirtualMachine = New-AzureRmVMConfig `
  -VMName $VmName `
  -VMSize $VmSize 

$VirtualMachine = Set-AzureRmVMOperatingSystem `
  -VM $VirtualMachine `
  -Windows `
  -ComputerName "MainComputer" `
  -Credential $Credential 

$VirtualMachine = Set-AzureRmVMSourceImage `
  -VM $VirtualMachine `
  -PublisherName "MicrosoftWindowsServer" `
  -Offer "WindowsServer" `
  -Skus "2016-Datacenter" `
  -Version "latest"

$osDiskName = "OsDisk"
$osDiskUri = '{0}vhds/{1}-{2}.vhd' -f `
  $StorageAccount.PrimaryEndpoints.Blob.ToString(),`
  $vmName.ToLower(), `
  $osDiskName

# Sets hello operating system disk properties on a virtual machine. 
$VirtualMachine = Set-AzureRmVMOSDisk `
  -VM $VirtualMachine `
  -Name $osDiskName `
  -VhdUri $OsDiskUri `
  -CreateOption FromImage | `
  Add-AzureRmVMNetworkInterface -Id $nic.Id 

#Create hello virtual machine.
New-AzureRmVM `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -VM $VirtualMachine
```

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="998c8-131">Conectar máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="998c8-131">Connect toohello virtual machine</span></span>

<span data-ttu-id="998c8-132">Después de que se crea correctamente la máquina virtual de hello, abra una máquina virtual de escritorio remoto conexión toohello desde el kit de desarrollo de hello, o desde un cliente externo basado en Windows si está conectado a través de VPN.</span><span class="sxs-lookup"><span data-stu-id="998c8-132">After hello virtual machine is successfully created, open a Remote Desktop connection toohello virtual machine from hello development kit, or from a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="998c8-133">tooremote en la máquina virtual de Hola que creó en el paso anterior de hello, necesita su dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="998c8-133">tooremote into hello virtual machine that you created in hello previous step, you need its public IP address.</span></span> <span data-ttu-id="998c8-134">Ejecute hello después comando tooget Hola dirección IP pública de la máquina virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="998c8-134">Run hello following command tooget hello public IP address of hello virtual machine:</span></span> 

```powershell
Get-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName | Select IpAddress
```
 
<span data-ttu-id="998c8-135">Siguiente Hola de uso del comando toocreate una sesión de escritorio remoto con la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="998c8-135">Use hello following command toocreate a Remote Desktop session with hello virtual machine.</span></span> <span data-ttu-id="998c8-136">Reemplace la dirección IP de Hola por hello publicIPAddress de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="998c8-136">Replace hello IP address with hello publicIPAddress of your virtual machine.</span></span> <span data-ttu-id="998c8-137">Cuando se le solicite, escriba Hola nombre de usuario y contraseña que utilizó al crear la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="998c8-137">When prompted, enter hello username and password that you used when creating hello virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```
## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="998c8-138">Eliminar la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="998c8-138">Delete hello virtual machine</span></span>

<span data-ttu-id="998c8-139">Cuando ya no necesite usar hello después el grupo de recursos de Hola de tooremove de comando que contiene la máquina virtual de Hola y sus recursos relacionados:</span><span class="sxs-lookup"><span data-stu-id="998c8-139">When no longer needed, use hello following command tooremove hello resource group that contains hello virtual machine and its related resources:</span></span>

```powershell
Remove-AzureRmResourceGroup `
  -Name $ResourceGroupName
```

## <a name="next-steps"></a><span data-ttu-id="998c8-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="998c8-140">Next steps</span></span>

<span data-ttu-id="998c8-141">toolearn acerca del almacenamiento en la pila de Azure, consulte toohello [Introducción al almacenamiento](azure-stack-storage-overview.md) tema.</span><span class="sxs-lookup"><span data-stu-id="998c8-141">toolearn about Storage in Azure Stack, refer toohello [storage overview](azure-stack-storage-overview.md) topic.</span></span>

