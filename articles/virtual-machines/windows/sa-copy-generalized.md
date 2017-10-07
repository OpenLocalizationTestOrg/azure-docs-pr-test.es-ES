---
title: aaaCreate una imagen no administrada de una VM generalizada en Azure | Documentos de Microsoft
description: "Crear una imagen no administrado de un generalizado toocreate toouse de máquina virtual de Windows varias copias de una máquina virtual en Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="fe282-103">Cómo toocreate una máquina virtual no administrada de la imagen de una VM de Azure</span><span class="sxs-lookup"><span data-stu-id="fe282-103">How toocreate an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="fe282-104">En este artículo se explica cómo usar cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fe282-104">This article covers using storage accounts.</span></span> <span data-ttu-id="fe282-105">Se recomienda utilizar Managed Disks e imágenes administradas en lugar de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fe282-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="fe282-106">Para más información, vea [Captura de una imagen administrada de una máquina virtual generalizada en Azure](capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="fe282-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="fe282-107">Este artículo muestra cómo toouse Azure PowerShell toocreate una imagen de una VM generalizada de Azure con una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fe282-107">This article shows you how toouse Azure PowerShell toocreate an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="fe282-108">A continuación, puede usar Hola imagen toocreate otra máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe282-108">You can then use hello image toocreate another VM.</span></span> <span data-ttu-id="fe282-109">imagen de Hello incluye el disco del sistema operativo de Hola y discos de datos de Hola que son la máquina virtual de toohello adjunto.</span><span class="sxs-lookup"><span data-stu-id="fe282-109">hello image includes hello OS disk and hello data disks that are attached toohello virtual machine.</span></span> <span data-ttu-id="fe282-110">imagen de Hello no incluye recursos de red virtual de hello, por lo que necesita tooset los recursos cuando creas Hola nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe282-110">hello image doesn't include hello virtual network resources, so you need tooset up those resources when you create hello new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fe282-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fe282-111">Prerequisites</span></span>
<span data-ttu-id="fe282-112">Necesita toohave PowerShell de Azure versión 1.0. x o posterior instalado.</span><span class="sxs-lookup"><span data-stu-id="fe282-112">You need toohave Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="fe282-113">Si aún no ha instalado PowerShell, lea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para los pasos de instalación.</span><span class="sxs-lookup"><span data-stu-id="fe282-113">If you haven't already installed PowerShell, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-hello-vm"></a><span data-ttu-id="fe282-114">Generalizar Hola VM</span><span class="sxs-lookup"><span data-stu-id="fe282-114">Generalize hello VM</span></span> 
<span data-ttu-id="fe282-115">Esta sección muestra cómo toogeneralize la máquina virtual de Windows para su uso como una imagen.</span><span class="sxs-lookup"><span data-stu-id="fe282-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="fe282-116">Generalizar una máquina virtual quita toda la información de cuenta personal, entre otras cosas y prepara Hola máquina toobe utilizado como una imagen.</span><span class="sxs-lookup"><span data-stu-id="fe282-116">Generalizing a VM removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="fe282-117">Para obtener más información acerca de Sysprep, consulte [cómo tooUse Sysprep: Introducción](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe282-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="fe282-118">Asegúrese de que los roles de servidor hello ejecutando en el equipo de hello son compatibles con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="fe282-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="fe282-119">Para más información, consulte [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="fe282-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe282-120">Si va a cargar el tooAzure de disco duro virtual para hello primera vez, asegúrese de que tiene [preparado la máquina virtual](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de ejecutar Sysprep.</span><span class="sxs-lookup"><span data-stu-id="fe282-120">If you are uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="fe282-121">También puede generalizar una VM de Linux con `sudo waagent -deprovision+user` y, a continuación, use PowerShell toocapture Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe282-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell toocapture hello VM.</span></span> <span data-ttu-id="fe282-122">Para obtener información acerca del uso de hello CLI toocapture una máquina virtual, consulte [cómo toogeneralize y la captura de una máquina virtual de Linux con hello Azure CLI ](../linux/capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="fe282-122">For information about using hello CLI toocapture a VM, see [How toogeneralize and capture a Linux virtual machine using hello Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="fe282-123">Inicie sesión en toohello máquina virtual de Windows.</span><span class="sxs-lookup"><span data-stu-id="fe282-123">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="fe282-124">Abra la ventana de símbolo del sistema de hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="fe282-124">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="fe282-125">Cambie el directorio de hello demasiado**%windir%\system32\sysprep**y, a continuación, ejecute `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="fe282-125">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="fe282-126">Hola **herramienta de preparación del sistema** cuadro de diálogo, seleccione **sistema Out-of-Box experiencia inmediata (OOBE)**y asegúrese de que ese hello **generalizar** casilla está activada.</span><span class="sxs-lookup"><span data-stu-id="fe282-126">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="fe282-127">En **Opciones de apagado**, seleccione **Apagar**.</span><span class="sxs-lookup"><span data-stu-id="fe282-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="fe282-128">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fe282-128">Click **OK**.</span></span>
   
    ![Iniciar Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="fe282-130">Cuando Sysprep finalice, se apaga máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe282-130">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="fe282-131">No se reinician Hola VM hasta que esté listo cargando tooAzure de disco duro virtual de Hola o crear una imagen de VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe282-131">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="fe282-132">Si obtiene reinicia Hola VM accidentalmente, ejecute Sysprep toogeneralize vuelva a.</span><span class="sxs-lookup"><span data-stu-id="fe282-132">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 

## <a name="log-in-tooazure-powershell"></a><span data-ttu-id="fe282-133">Inicie sesión en tooAzure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe282-133">Log in tooAzure PowerShell</span></span>
1. <span data-ttu-id="fe282-134">Abra PowerShell de Azure e inicie sesión tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe282-134">Open Azure PowerShell and sign in tooyour Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="fe282-135">Abre una ventana emergente para tooenter sus credenciales de cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe282-135">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
2. <span data-ttu-id="fe282-136">Obtener identificadores de suscripción de Hola para las suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="fe282-136">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="fe282-137">Conjunto Hola suscripción correcta con el identificador de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe282-137">Set hello correct subscription using hello subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a><span data-ttu-id="fe282-138">Cancela la asignación de hello VM y establezca Hola estado toogeneralized</span><span class="sxs-lookup"><span data-stu-id="fe282-138">Deallocate hello VM and set hello state toogeneralized</span></span>
1. <span data-ttu-id="fe282-139">Cancela la asignación de recursos de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe282-139">Deallocate hello VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="fe282-140">Hola *estado* para hello VM en hello Azure portal cambia de **detenido** demasiado**detenido (desasignado)**.</span><span class="sxs-lookup"><span data-stu-id="fe282-140">hello *Status* for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="fe282-141">Establecer el estado de saludo de la máquina virtual de hello demasiado**generalizado**.</span><span class="sxs-lookup"><span data-stu-id="fe282-141">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="fe282-142">Comprobar estado de Hola de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe282-142">Check hello status of hello VM.</span></span> <span data-ttu-id="fe282-143">Hola **OSState/generalizar** sección para hello VM debe tener hello **DisplayStatus** establecido demasiado**VM generalizado**.</span><span class="sxs-lookup"><span data-stu-id="fe282-143">hello **OSState/generalized** section for hello VM should have hello **DisplayStatus** set too**VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a><span data-ttu-id="fe282-144">Crear imagen de Hola</span><span class="sxs-lookup"><span data-stu-id="fe282-144">Create hello image</span></span>

<span data-ttu-id="fe282-145">Crear una imagen de máquina virtual no administrado en el contenedor de almacenamiento de destino de hello con este comando.</span><span class="sxs-lookup"><span data-stu-id="fe282-145">Create an unmanaged virtual machine image in hello destination storage container using this command.</span></span> <span data-ttu-id="fe282-146">Hello imagen se crea en Hola misma cuenta de almacenamiento como Hola máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="fe282-146">hello image is created in hello same storage account as hello original virtual machine.</span></span> <span data-ttu-id="fe282-147">Hola `-Path` parámetro guarda una copia de la plantilla JSON de Hola Hola equipo de origen VM tooyour local.</span><span class="sxs-lookup"><span data-stu-id="fe282-147">hello `-Path` parameter saves a copy of hello JSON template for hello source VM tooyour local computer.</span></span> <span data-ttu-id="fe282-148">Hola `-DestinationContainerName` parámetro es Hola nombre del contenedor de Hola que desea toohold las imágenes.</span><span class="sxs-lookup"><span data-stu-id="fe282-148">hello `-DestinationContainerName` parameter is hello name of hello container that you want toohold your images.</span></span> <span data-ttu-id="fe282-149">Si no existe el contenedor de hello, se crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="fe282-149">If hello container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="fe282-150">Puede obtener dirección URL de hello de la imagen de plantilla de archivos de hello JSON.</span><span class="sxs-lookup"><span data-stu-id="fe282-150">You can get hello URL of your image from hello JSON file template.</span></span> <span data-ttu-id="fe282-151">Vaya toohello **recursos** > **storageProfile** > **osDisk** > **imagen**  >  **uri** sección de ruta de acceso completa de saludo de la imagen.</span><span class="sxs-lookup"><span data-stu-id="fe282-151">Go toohello **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for hello complete path of your image.</span></span> <span data-ttu-id="fe282-152">dirección URL de Hola de imagen de hello es similar: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="fe282-152">hello URL of hello image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="fe282-153">También puede comprobar Hola URI en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe282-153">You can also verify hello URI in hello portal.</span></span> <span data-ttu-id="fe282-154">imagen de Hello es contenedor tooa copiada denominado **system** en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fe282-154">hello image is copied tooa container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-hello-image"></a><span data-ttu-id="fe282-155">Crear una máquina virtual a partir de la imagen de Hola</span><span class="sxs-lookup"><span data-stu-id="fe282-155">Create a VM from hello image</span></span>

<span data-ttu-id="fe282-156">Ahora puede crear una o más máquinas virtuales de imagen de hello no administrado.</span><span class="sxs-lookup"><span data-stu-id="fe282-156">Now you can create one or more VMs from hello unmanaged image.</span></span>

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="fe282-157">Hola de conjunto de URI de hello VHD</span><span class="sxs-lookup"><span data-stu-id="fe282-157">Set hello URI of hello VHD</span></span>

<span data-ttu-id="fe282-158">Hola URI para hello toouse de disco duro virtual está en formato de hello: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span><span class="sxs-lookup"><span data-stu-id="fe282-158">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="fe282-159">En este ejemplo Hola VHD denominada **myVHD** está en la cuenta de almacenamiento de hello **mystorageaccount** en el contenedor de hello **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="fe282-159">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="fe282-160">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="fe282-160">Create a virtual network</span></span>
<span data-ttu-id="fe282-161">Crear red virtual de Hola y de las subredes de hello [red virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe282-161">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="fe282-162">Crear una subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe282-162">Create hello subnet.</span></span> <span data-ttu-id="fe282-163">Hello en el ejemplo siguiente crea una subred denominada **mySubnet** en grupo de recursos de hello **myResourceGroup** con prefijo de dirección de hello **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="fe282-163">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="fe282-164">Crear red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe282-164">Create hello virtual network.</span></span> <span data-ttu-id="fe282-165">Hello en el ejemplo siguiente crea una red virtual con el nombre **myVnet** Hola **West US** ubicación con el prefijo de dirección de hello **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="fe282-165">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="fe282-166">Creación de una dirección IP y una interfaz de red</span><span class="sxs-lookup"><span data-stu-id="fe282-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="fe282-167">tooenable la comunicación con la máquina virtual de hello en la red virtual de hello, necesita un [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) y una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="fe282-167">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="fe282-168">Cree una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="fe282-168">Create a public IP address.</span></span> <span data-ttu-id="fe282-169">Este ejemplo crea una dirección IP pública denominada "**myPip**".</span><span class="sxs-lookup"><span data-stu-id="fe282-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="fe282-170">Crear NIC de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe282-170">Create hello NIC.</span></span> <span data-ttu-id="fe282-171">Este ejemplo crea una NIC denominada "**myNic**".</span><span class="sxs-lookup"><span data-stu-id="fe282-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="fe282-172">Crear grupo de seguridad de red de hello y una regla de RDP</span><span class="sxs-lookup"><span data-stu-id="fe282-172">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="fe282-173">toobe puede toolog en tooyour VM mediante RDP, deberá toohave una regla de seguridad que permite el acceso RDP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="fe282-173">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="fe282-174">Este ejemplo crea un NSG denominado"**myNsg**" que contiene una regla llamada "**myRdpRule**" que permita el tráfico RDP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="fe282-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="fe282-175">Para obtener más información acerca de los NSG, consulte [abrir puertos tooa VM en Azure con PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe282-175">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="fe282-176">Cree una variable para la red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="fe282-176">Create a variable for hello virtual network</span></span>
<span data-ttu-id="fe282-177">Cree una variable para la red virtual de hello completado.</span><span class="sxs-lookup"><span data-stu-id="fe282-177">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="fe282-178">Crear hello VM</span><span class="sxs-lookup"><span data-stu-id="fe282-178">Create hello VM</span></span>
<span data-ttu-id="fe282-179">Hello PowerShell siguiente completa de configuraciones de máquina virtual de Hola y usa imagen no administrado como origen de Hola para instalación nueva de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe282-179">hello following PowerShell completes hello virtual machine configurations and uses unmanaged image as hello source for hello new installation.</span></span>

</br>

```powershell
    # Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="fe282-180">Compruebe que se creó la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="fe282-180">Verify that hello VM was created</span></span>
<span data-ttu-id="fe282-181">Cuando haya finalizado, debería ver Hola recién creado VM hello [portal de Azure](https://portal.azure.com) en **examinar** > **máquinas virtuales**, o mediante Hola siguiente Comandos de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fe282-181">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="fe282-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fe282-182">Next steps</span></span>
<span data-ttu-id="fe282-183">toomanage la nueva máquina virtual con PowerShell de Azure, consulte [administrar máquinas virtuales con el Administrador de recursos de Azure y PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe282-183">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


