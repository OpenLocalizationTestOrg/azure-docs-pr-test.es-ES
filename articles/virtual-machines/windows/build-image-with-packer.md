---
title: "aaaHow toocreate imágenes de máquina virtual de Windows Azure con compresor | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse imágenes de toocreate compresor de máquinas virtuales de Windows en Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: d310fae3becb453b52d21281cb8ac53fa14a3fc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-windows-virtual-machine-images-in-azure"></a><span data-ttu-id="bf3bb-103">Cómo imágenes de máquina virtual de toouse compresor toocreate Windows de Azure</span><span class="sxs-lookup"><span data-stu-id="bf3bb-103">How toouse Packer toocreate Windows virtual machine images in Azure</span></span>
<span data-ttu-id="bf3bb-104">Cada máquina virtual (VM) en Azure se crea a partir de una imagen que define la distribución de Windows hello y versión del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-104">Each virtual machine (VM) in Azure is created from an image that defines hello Windows distribution and OS version.</span></span> <span data-ttu-id="bf3bb-105">Las imágenes pueden incluir configuraciones y aplicaciones preinstaladas.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="bf3bb-106">Hello Azure Marketplace proporciona muchas imágenes primeros y tercero para el sistema operativo de más comunes y los entornos de aplicaciones, o puede crear sus propias necesidades de tooyour imágenes personalizadas adaptadas.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-106">hello Azure Marketplace provides many first and third-party images for most common OS' and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="bf3bb-107">Este artículo detalla cómo toouse Hola Abrir herramienta de código fuente [compresor](https://www.packer.io/) toodefine y compilación imágenes personalizadas en Azure.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="bf3bb-108">Creación del grupo de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="bf3bb-108">Create Azure resource group</span></span>
<span data-ttu-id="bf3bb-109">Durante el proceso de compilación de hello, compresor crea recursos de Azure temporales cuando genera una VM de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="bf3bb-110">toocapture que son origen de máquina virtual para su uso como una imagen, debe definir un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="bf3bb-111">Hello resultado del proceso de compilación de compresor Hola se almacena en este grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="bf3bb-112">Cree un grupo de recursos con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="bf3bb-112">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="bf3bb-113">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="bf3bb-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a><span data-ttu-id="bf3bb-114">Creación de credenciales de Azure</span><span class="sxs-lookup"><span data-stu-id="bf3bb-114">Create Azure credentials</span></span>
<span data-ttu-id="bf3bb-115">Packer se autentica con Azure mediante una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="bf3bb-116">Las entidades de servicio de Azure son identidades de seguridad que pueden usarse con aplicaciones, servicios y herramientas de automatización como Packer.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="bf3bb-117">Controlar y definir permisos de hello como entidad de servicio de hello toowhat operaciones puede llevar a cabo en Azure.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="bf3bb-118">Crear un servicio principal con [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) y asignar permisos para toocreate de entidad de seguridad de servicio de Hola y administrar recursos con [AzureRmRoleAssignment New](/powershell/module/azurerm.resources/new-azurermroleassignment):</span><span class="sxs-lookup"><span data-stu-id="bf3bb-118">Create a service principal with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) and assign permissions for hello service principal toocreate and manage resources with [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span></span>

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="bf3bb-119">tooauthenticate tooAzure, también debe tooobtain los identificadores de inquilino y suscripción de Azure con [AzureRmSubscription Get](/powershell/module/azurerm.profile/get-azurermsubscription):</span><span class="sxs-lookup"><span data-stu-id="bf3bb-119">tooauthenticate tooAzure, you also need tooobtain your Azure tenant and subscription IDs with [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span></span>

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

<span data-ttu-id="bf3bb-120">Use estas dos identificadores en el paso siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-120">You use these two IDs in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="bf3bb-121">Definición de la plantilla de Packer</span><span class="sxs-lookup"><span data-stu-id="bf3bb-121">Define Packer template</span></span>
<span data-ttu-id="bf3bb-122">toobuild imágenes, crear una plantilla como un archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-122">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="bf3bb-123">En la plantilla de hello, defina los generadores y provisioners que efectúan Hola real de proceso de compilación.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-123">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="bf3bb-124">Compresor tiene un [aprovisionador para Azure](https://www.packer.io/docs/builders/azure.html) que le permite toodefine Azure recursos, como credenciales principal del servicio Hola creados en hello anterior paso.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-124">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="bf3bb-125">Cree un archivo denominado *windows.json* y pegar Hola siguen contenido.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-125">Create a file named *windows.json* and paste hello following content.</span></span> <span data-ttu-id="bf3bb-126">Escriba sus propios valores para siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="bf3bb-126">Enter your own values for hello following:</span></span>

| <span data-ttu-id="bf3bb-127">Parámetro</span><span class="sxs-lookup"><span data-stu-id="bf3bb-127">Parameter</span></span>                           | <span data-ttu-id="bf3bb-128">Donde tooobtain</span><span class="sxs-lookup"><span data-stu-id="bf3bb-128">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="bf3bb-129">*client_id*</span><span class="sxs-lookup"><span data-stu-id="bf3bb-129">*client_id*</span></span>                         | <span data-ttu-id="bf3bb-130">Vea el identificador de la entidad de servicio con `$sp.applicationId`</span><span class="sxs-lookup"><span data-stu-id="bf3bb-130">View service principal ID with `$sp.applicationId`</span></span> |
| <span data-ttu-id="bf3bb-131">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="bf3bb-131">*client_secret*</span></span>                     | <span data-ttu-id="bf3bb-132">La contraseña que especificó en `$securePassword`</span><span class="sxs-lookup"><span data-stu-id="bf3bb-132">Password you specified in `$securePassword`</span></span> |
| <span data-ttu-id="bf3bb-133">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="bf3bb-133">*tenant_id*</span></span>                         | <span data-ttu-id="bf3bb-134">Salida del comando `$sub.TenantId`</span><span class="sxs-lookup"><span data-stu-id="bf3bb-134">Output from `$sub.TenantId` command</span></span> |
| <span data-ttu-id="bf3bb-135">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="bf3bb-135">*subscription_id*</span></span>                   | <span data-ttu-id="bf3bb-136">Salida del comando `$sub.SubscriptionId`</span><span class="sxs-lookup"><span data-stu-id="bf3bb-136">Output from `$sub.SubscriptionId` command</span></span> |
| <span data-ttu-id="bf3bb-137">*object_id*</span><span class="sxs-lookup"><span data-stu-id="bf3bb-137">*object_id*</span></span>                         | <span data-ttu-id="bf3bb-138">Vea el identificador del objeto de la entidad de servicio con `$sp.Id`</span><span class="sxs-lookup"><span data-stu-id="bf3bb-138">View service principal object ID with `$sp.Id`</span></span> |
| <span data-ttu-id="bf3bb-139">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="bf3bb-139">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="bf3bb-140">Nombre del grupo de recursos que creó en el primer paso de Hola</span><span class="sxs-lookup"><span data-stu-id="bf3bb-140">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="bf3bb-141">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="bf3bb-141">*managed_image_name*</span></span>                | <span data-ttu-id="bf3bb-142">Nombre de imagen de disco administrado Hola que se crea</span><span class="sxs-lookup"><span data-stu-id="bf3bb-142">Name for hello managed disk image that is created</span></span> |

```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "0831b578-8ab6-40b9-a581-9a880a94aab1",
    "client_secret": "P@ssw0rd!",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",
    "object_id": "a7dfb070-0d5b-47ac-b9a5-cf214fff0ae2",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Windows",
    "image_publisher": "MicrosoftWindowsServer",
    "image_offer": "WindowsServer",
    "image_sku": "2016-Datacenter",

    "communicator": "winrm",
    "winrm_use_ssl": "true",
    "winrm_insecure": "true",
    "winrm_timeout": "3m",
    "winrm_username": "packer",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "type": "powershell",
    "inline": [
      "Add-WindowsFeature Web-Server",
      "if( Test-Path $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml ){ rm $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml -Force}",
      "& $Env:SystemRoot\\System32\\Sysprep\\Sysprep.exe /oobe /generalize /shutdown /quiet"
    ]
  }]
}
```

<span data-ttu-id="bf3bb-143">Esta plantilla crea una máquina virtual de Windows Server 2016, instala IIS y generaliza Hola VM con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-143">This template builds a Windows Server 2016 VM, installs IIS, then generalizes hello VM with Sysprep.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="bf3bb-144">Creación de una imagen de Packer</span><span class="sxs-lookup"><span data-stu-id="bf3bb-144">Build Packer image</span></span>
<span data-ttu-id="bf3bb-145">Si no se ha instalado en el equipo local, de compresor [siga las instrucciones de instalación de compresor hello](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="bf3bb-145">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="bf3bb-146">Crear imagen de Hola especificando el compresor archivo de plantilla como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="bf3bb-146">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build windows.json
```

<span data-ttu-id="bf3bb-147">Un ejemplo de salida de hello de hello anterior comandos es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="bf3bb-147">An example of hello output from hello preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> task : Image deployment
==> azure-arm:  ->> dept : Engineering
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello certificate’s URL ...
==> azure-arm:  -> Key Vault Name        : ‘pkrkvpq0mthtbtt’
==> azure-arm:  -> Key Vault Secret Name : ‘packerKeyVaultSecret’
==> azure-arm:  -> Certificate URL       : ‘https://pkrkvpq0mthtbtt.vault.azure.net/secrets/packerKeyVaultSecret/8c7bd823e4fa44e1abb747636128adbb'
==> azure-arm: Setting hello certificate’s URL ...
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.55.35’
==> azure-arm: Waiting for WinRM toobecome available...
==> azure-arm: Connected tooWinRM!
==> azure-arm: Provisioning with Powershell...
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-powershell-provisioner902510110
    azure-arm: #< CLIXML
    azure-arm:
    azure-arm: Success Restart Needed Exit Code      Feature Result
    azure-arm: ------- -------------- ---------      --------------
    azure-arm: True    No             Success        {Common HTTP Features, Default Document, D...
    azure-arm: <Objs Version=“1.1.0.1” xmlns=“http://schemas.microsoft.com/powershell/2004/04"><Obj S=“progress” RefId=“0"><TN RefId=“0”><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N=“SourceId”>1</I64><PR N=“Record”><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-pq0mthtbtt/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Compute Name              : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```

<span data-ttu-id="bf3bb-148">Tarda unos minutos para hello de toobuild de compresor de máquina virtual, ejecute a provisioners hello y una implementación de Hola de limpieza.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-148">It takes a few minutes for Packer toobuild hello VM, run hello provisioners, and clean up hello deployment.</span></span>


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="bf3bb-149">Creación de una máquina virtual desde una imagen de Azure</span><span class="sxs-lookup"><span data-stu-id="bf3bb-149">Create VM from Azure Image</span></span>
<span data-ttu-id="bf3bb-150">Establecer un administrador username y password para máquinas virtuales de hello con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span><span class="sxs-lookup"><span data-stu-id="bf3bb-150">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="bf3bb-151">Ya puede crear una máquina virtual a partir de la imagen con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="bf3bb-151">You can now create a VM from your Image with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="bf3bb-152">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM* de *myPackerImage*.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-152">hello following example creates a VM named *myVM* from *myPackerImage*.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod "Static" `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

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
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Define hello image created by Packer
$image = Get-AzureRMImage -ImageName myPackerImage -ResourceGroupName $rgName

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -Id $image.Id | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```

<span data-ttu-id="bf3bb-153">Se tarda unos minutos toocreate Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-153">It takes a few minutes toocreate hello VM.</span></span>


## <a name="test-vm-and-iis"></a><span data-ttu-id="bf3bb-154">Pruebas de la máquina virtual y de IIS</span><span class="sxs-lookup"><span data-stu-id="bf3bb-154">Test VM and IIS</span></span>
<span data-ttu-id="bf3bb-155">Obtener dirección IP pública de saludo de la máquina virtual con [AzureRmPublicIPAddress Get](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="bf3bb-155">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="bf3bb-156">Hello en el ejemplo siguiente se obtiene la dirección IP de Hola para *myPublicIP* creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="bf3bb-156">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="bf3bb-157">A continuación, puede escribir la dirección IP pública hello en el Explorador de web tooa.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-157">You can then enter hello public IP address in tooa web browser.</span></span>

![Sitio predeterminado de IIS](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a><span data-ttu-id="bf3bb-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bf3bb-159">Next steps</span></span>
<span data-ttu-id="bf3bb-160">En este ejemplo, ha utilizado compresor toocreate una imagen de VM con IIS instalados.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-160">In this example, you used Packer toocreate a VM image with IIS already installed.</span></span> <span data-ttu-id="bf3bb-161">Puede usar esta imagen de máquina virtual junto con los flujos de trabajo existente de implementación, como toodeploy su tooVMs de aplicación creado a partir de hello imagen con Team Services, Ansible, Chef o Puppet.</span><span class="sxs-lookup"><span data-stu-id="bf3bb-161">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Team Services, Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="bf3bb-162">Para ver más plantillas de Packer de ejemplo para otras distribuciones de Windows, consulte [este repositorio de GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="bf3bb-162">For additional example Packer templates for other Windows distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>