---
title: "Creación de una imagen no administrada de una máquina virtual generalizada en Azure | Microsoft Docs"
description: "Cree una imagen no administrada de una máquina virtual de Windows generalizada a fin de utilizarla para crear varias copias de una máquina virtual en Azure."
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
ms.openlocfilehash: d7f4a9558175835eba9096e6845726f21c7459d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-create-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="33352-103">Creación de una imagen de máquina virtual no administrada a partir de una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="33352-103">How to create an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="33352-104">En este artículo se explica cómo usar cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="33352-104">This article covers using storage accounts.</span></span> <span data-ttu-id="33352-105">Se recomienda utilizar Managed Disks e imágenes administradas en lugar de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="33352-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="33352-106">Para más información, vea [Captura de una imagen administrada de una máquina virtual generalizada en Azure](capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="33352-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="33352-107">En este artículo se muestra cómo usar Azure PowerShell para crear una imagen de una máquina virtual de Azure generalizada con una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="33352-107">This article shows you how to use Azure PowerShell to create an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="33352-108">Después, puede usar la imagen para crear otra máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="33352-108">You can then use the image to create another VM.</span></span> <span data-ttu-id="33352-109">Dicha imagen incluye el disco del SO y los discos de datos conectados a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="33352-109">The image includes the OS disk and the data disks that are attached to the virtual machine.</span></span> <span data-ttu-id="33352-110">La imagen no incluye los recursos de red virtual, por lo que tiene que es preciso configurarlos al crear la máquina virtual nueva.</span><span class="sxs-lookup"><span data-stu-id="33352-110">The image doesn't include the virtual network resources, so you need to set up those resources when you create the new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="33352-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="33352-111">Prerequisites</span></span>
<span data-ttu-id="33352-112">Es preciso tener instalada la versión 1.0.x de Azure PowerShell, o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="33352-112">You need to have Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="33352-113">Si aún no ha instalado PowerShell, lea [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) para ver los pasos de instalación.</span><span class="sxs-lookup"><span data-stu-id="33352-113">If you haven't already installed PowerShell, read [How to install and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-the-vm"></a><span data-ttu-id="33352-114">Generalización de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="33352-114">Generalize the VM</span></span> 
<span data-ttu-id="33352-115">En esta sección se muestra cómo generalizar la máquina virtual Windows para usarla como imagen.</span><span class="sxs-lookup"><span data-stu-id="33352-115">This section shows you how to generalize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="33352-116">La generalización de una máquina virtual elimina toda la información personal de la cuenta, entre otras cosas, y prepara la máquina para usarse como imagen.</span><span class="sxs-lookup"><span data-stu-id="33352-116">Generalizing a VM removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="33352-117">Para obtener más información sobre Sysprep, vea [Uso de Sysprep: Introducción](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="33352-117">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="33352-118">Asegúrese de que los roles de servidor que se ejecutan en la máquina sean compatibles con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="33352-118">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="33352-119">Para más información, consulte [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="33352-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="33352-120">Si va a cargar el VHD en Azure por primera vez, asegúrese de que tiene [preparada la máquina virtual](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de ejecutar Sysprep.</span><span class="sxs-lookup"><span data-stu-id="33352-120">If you are uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="33352-121">También puede generalizar una máquina virtual Linux con `sudo waagent -deprovision+user` y, luego, usar PowerShell para capturar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="33352-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell to capture the VM.</span></span> <span data-ttu-id="33352-122">Para obtener información sobre cómo usar la CLI para capturar una máquina virtual, vea el artículo sobre [cómo generalizar y capturar una máquina virtual Linux mediante la CLI de Azure](../linux/capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="33352-122">For information about using the CLI to capture a VM, see [How to generalize and capture a Linux virtual machine using the Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="33352-123">Inicie sesión en la máquina virtual de Windows.</span><span class="sxs-lookup"><span data-stu-id="33352-123">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="33352-124">Abra una ventana del símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="33352-124">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="33352-125">Cambie el directorio a **%windir%\system32\sysprep** y, después, ejecute `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="33352-125">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="33352-126">En **Herramienta de preparación del sistema**, seleccione **Iniciar la Configuración rápida (OOBE)** y asegúrese de que la casilla **Generalizar** está activada.</span><span class="sxs-lookup"><span data-stu-id="33352-126">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="33352-127">En **Opciones de apagado**, seleccione **Apagar**.</span><span class="sxs-lookup"><span data-stu-id="33352-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="33352-128">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="33352-128">Click **OK**.</span></span>
   
    ![Iniciar Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="33352-130">Cuando Sysprep finaliza, apaga la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="33352-130">When Sysprep completes, it shuts down the virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="33352-131">No reinicie la máquina virtual hasta que haya terminado de cargar el VHD en Azure o de crear una imagen de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="33352-131">Do not restart the VM until you are done uploading the VHD to Azure or creating an image from the VM.</span></span> <span data-ttu-id="33352-132">Si la máquina virtual se reinicia accidentalmente, ejecute Sysprep para generalizarla de nuevo.</span><span class="sxs-lookup"><span data-stu-id="33352-132">If the VM accidentally gets restarted, run Sysprep to generalize it again.</span></span>
> 
> 

## <a name="log-in-to-azure-powershell"></a><span data-ttu-id="33352-133">Iniciar sesión en Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="33352-133">Log in to Azure PowerShell</span></span>
1. <span data-ttu-id="33352-134">Abra Azure PowerShell e inicie sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="33352-134">Open Azure PowerShell and sign in to your Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="33352-135">Se abrirá una ventana emergente para que escriba sus credenciales de cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="33352-135">A pop-up window opens for you to enter your Azure account credentials.</span></span>
2. <span data-ttu-id="33352-136">Obtenga los identificadores de suscripción para las suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="33352-136">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="33352-137">Establezca la suscripción correcta con el identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="33352-137">Set the correct subscription using the subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-the-vm-and-set-the-state-to-generalized"></a><span data-ttu-id="33352-138">Desasignar la máquina virtual y establecer el estado en generalizado</span><span class="sxs-lookup"><span data-stu-id="33352-138">Deallocate the VM and set the state to generalized</span></span>
1. <span data-ttu-id="33352-139">Desasigne los recursos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="33352-139">Deallocate the VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="33352-140">El *estado* de la máquina virtual en Azure Portal cambia de **Detenido** a **Detenido (desasignado)**.</span><span class="sxs-lookup"><span data-stu-id="33352-140">The *Status* for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="33352-141">Establezca el estado de la máquina virtual en **Generalizado**.</span><span class="sxs-lookup"><span data-stu-id="33352-141">Set the status of the virtual machine to **Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="33352-142">Compruebe el estado de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="33352-142">Check the status of the VM.</span></span> <span data-ttu-id="33352-143">En la sección **OSState/generalized** de la máquina virtual, **DisplayStatus** debe estar establecido en **VM generalized** (Máquina virtual generalizada).</span><span class="sxs-lookup"><span data-stu-id="33352-143">The **OSState/generalized** section for the VM should have the **DisplayStatus** set to **VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-the-image"></a><span data-ttu-id="33352-144">Crear la imagen</span><span class="sxs-lookup"><span data-stu-id="33352-144">Create the image</span></span>

<span data-ttu-id="33352-145">Cree una imagen de máquina virtual no administrada en el contenedor de almacenamiento de destino con este comando.</span><span class="sxs-lookup"><span data-stu-id="33352-145">Create an unmanaged virtual machine image in the destination storage container using this command.</span></span> <span data-ttu-id="33352-146">La imagen se crea en la misma cuenta de almacenamiento que la de la máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="33352-146">The image is created in the same storage account as the original virtual machine.</span></span> <span data-ttu-id="33352-147">El parámetro `-Path` guarda una copia de la plantilla JSON para la máquina virtual de origen en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="33352-147">The `-Path` parameter saves a copy of the JSON template for the source VM to your local computer.</span></span> <span data-ttu-id="33352-148">El parámetro `-DestinationContainerName` es el nombre del contenedor que desea que contenga las imágenes.</span><span class="sxs-lookup"><span data-stu-id="33352-148">The `-DestinationContainerName` parameter is the name of the container that you want to hold your images.</span></span> <span data-ttu-id="33352-149">Si el contenedor no existe, se creará.</span><span class="sxs-lookup"><span data-stu-id="33352-149">If the container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="33352-150">Puede obtener la dirección URL de la imagen de la plantilla del archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="33352-150">You can get the URL of your image from the JSON file template.</span></span> <span data-ttu-id="33352-151">Vaya a la sección **recursos** > **storageProfile** > **osDisk** > **imagen** > **uri** para ver la ruta de acceso completa de la imagen.</span><span class="sxs-lookup"><span data-stu-id="33352-151">Go to the **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for the complete path of your image.</span></span> <span data-ttu-id="33352-152">La dirección URL de la imagen es similar a esta: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="33352-152">The URL of the image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="33352-153">También puede comprobar el URI en el portal.</span><span class="sxs-lookup"><span data-stu-id="33352-153">You can also verify the URI in the portal.</span></span> <span data-ttu-id="33352-154">La imagen se copia en un contenedor denominado **system** de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="33352-154">The image is copied to a container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-the-image"></a><span data-ttu-id="33352-155">Creación de una máquina virtual a partir de una imagen</span><span class="sxs-lookup"><span data-stu-id="33352-155">Create a VM from the image</span></span>

<span data-ttu-id="33352-156">Ahora puede crear una o varias máquinas virtuales a partir de la imagen no administrada.</span><span class="sxs-lookup"><span data-stu-id="33352-156">Now you can create one or more VMs from the unmanaged image.</span></span>

### <a name="set-the-uri-of-the-vhd"></a><span data-ttu-id="33352-157">Establecimiento del URI del VHD</span><span class="sxs-lookup"><span data-stu-id="33352-157">Set the URI of the VHD</span></span>

<span data-ttu-id="33352-158">El URI para el VHD que se usará está en el formato: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span><span class="sxs-lookup"><span data-stu-id="33352-158">The URI for the VHD to use is in the format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="33352-159">En este ejemplo, el VHD denominado "**myVHD**" es la cuenta de almacenamiento **mystorageaccount** del contenedor **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="33352-159">In this example the VHD named **myVHD** is in the storage account **mystorageaccount** in the container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="33352-160">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="33352-160">Create a virtual network</span></span>
<span data-ttu-id="33352-161">Cree la red virtual y la subred de la [red virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="33352-161">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="33352-162">Cree la subred.</span><span class="sxs-lookup"><span data-stu-id="33352-162">Create the subnet.</span></span> <span data-ttu-id="33352-163">El ejemplo siguiente crea una subred denominada "**mySubnet**" en el grupo de recursos "**myResourceGroup**" con el prefijo de dirección **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="33352-163">The following sample creates a subnet named **mySubnet** in the resource group **myResourceGroup** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="33352-164">Creación de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="33352-164">Create the virtual network.</span></span> <span data-ttu-id="33352-165">El ejemplo siguiente crea una red virtual denominada "**myVnet**" en la ubicación **oeste de EE. UU.** con el prefijo de dirección **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="33352-165">The following sample creates a virtual network named **myVnet** in the **West US** location with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="33352-166">Creación de una dirección IP y una interfaz de red</span><span class="sxs-lookup"><span data-stu-id="33352-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="33352-167">Para permitir la comunicación con la máquina virtual en la red virtual, necesitará una [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) y una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="33352-167">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="33352-168">Cree una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="33352-168">Create a public IP address.</span></span> <span data-ttu-id="33352-169">Este ejemplo crea una dirección IP pública denominada "**myPip**".</span><span class="sxs-lookup"><span data-stu-id="33352-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="33352-170">Cree la NIC.</span><span class="sxs-lookup"><span data-stu-id="33352-170">Create the NIC.</span></span> <span data-ttu-id="33352-171">Este ejemplo crea una NIC denominada "**myNic**".</span><span class="sxs-lookup"><span data-stu-id="33352-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="33352-172">Creación del grupo de seguridad de red y las reglas de RDP</span><span class="sxs-lookup"><span data-stu-id="33352-172">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="33352-173">Para poder iniciar sesión en la máquina virtual mediante RDP, debe tener una regla de seguridad que permita el acceso RDP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="33352-173">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="33352-174">Este ejemplo crea un NSG denominado"**myNsg**" que contiene una regla llamada "**myRdpRule**" que permita el tráfico RDP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="33352-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="33352-175">Para obtener más información sobre NSG, consulte [Apertura de puertos para una máquina virtual en Azure mediante PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="33352-175">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="33352-176">Creación de una variable para la red virtual</span><span class="sxs-lookup"><span data-stu-id="33352-176">Create a variable for the virtual network</span></span>
<span data-ttu-id="33352-177">Cree una variable para la red virtual completada.</span><span class="sxs-lookup"><span data-stu-id="33352-177">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-the-vm"></a><span data-ttu-id="33352-178">Creación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="33352-178">Create the VM</span></span>
<span data-ttu-id="33352-179">El siguiente script de PowerShell completa las configuraciones de la máquina virtual y usa una imagen no administrada como origen para la nueva instalación.</span><span class="sxs-lookup"><span data-stu-id="33352-179">The following PowerShell completes the virtual machine configurations and uses unmanaged image as the source for the new installation.</span></span>

</br>

```powershell
    # Enter a new user name and password to use as the local administrator account 
    # for remotely accessing the VM.
    $cred = Get-Credential

    # Name of the storage account where the VHD is located. This example sets the 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of the virtual machine. This example sets the VM name as "myVM".
    $vmName = "myVM"

    # Size of the virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See the VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for the VM. This examples sets the computer name as "myComputer".
    $computerName = "myComputer"

    # Name of the disk that holds the OS. This example sets the 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets the SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get the storage account where the uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set the VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set the Windows operating system configuration and add the NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create the OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure the OS disk to be created from the existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create the new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="33352-180">Comprobación de que se creó la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="33352-180">Verify that the VM was created</span></span>
<span data-ttu-id="33352-181">Cuando finalice, debería ver la máquina virtual recién creada en el [Azure Portal](https://portal.azure.com), en **Examinar** > **Máquinas virtuales** o mediante los comandos de PowerShell siguientes:</span><span class="sxs-lookup"><span data-stu-id="33352-181">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="33352-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="33352-182">Next steps</span></span>
<span data-ttu-id="33352-183">Para administrar la nueva máquina virtual de Azure PowerShell, consulte [Administración de máquinas virtuales de Azure con Resource Manager y PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="33352-183">To manage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


