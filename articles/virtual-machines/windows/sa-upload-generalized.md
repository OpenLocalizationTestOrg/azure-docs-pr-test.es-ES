---
title: "aaaUpload un toocreate de disco duro virtual de generalizar varias máquinas virtuales en Azure | Documentos de Microsoft"
description: "Cargar un toocreate de cuenta de almacenamiento de Azure de tooan de disco duro virtual generalizado un toouse de máquina virtual de Windows con el modelo de implementación del Administrador de recursos de Hola."
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
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a><span data-ttu-id="447b5-103">Cargar un toocreate tooAzure de disco duro virtual generalizado una nueva máquina virtual</span><span class="sxs-lookup"><span data-stu-id="447b5-103">Upload a generalized VHD tooAzure toocreate a new VM</span></span>

<span data-ttu-id="447b5-104">Este tema tratan cargando una cuenta de almacenamiento de disco no administrado generalizado tooa y, a continuación, crear una nueva máquina virtual con el disco de hello cargado.</span><span class="sxs-lookup"><span data-stu-id="447b5-104">This topic covers uploading a generalized unmanaged disk tooa storage account and then creating a new VM using hello uploaded disk.</span></span> <span data-ttu-id="447b5-105">Con Sysprep se elimina toda la información personal de la cuenta de una imagen de un VHD generalizado.</span><span class="sxs-lookup"><span data-stu-id="447b5-105">A generalized VHD image has had all of your personal account information removed using Sysprep.</span></span> 

<span data-ttu-id="447b5-106">Si desea toocreate una máquina virtual desde un disco duro virtual especializada en una cuenta de almacenamiento, consulte [crear una máquina virtual desde un disco duro virtual especializado](sa-create-vm-specialized.md).</span><span class="sxs-lookup"><span data-stu-id="447b5-106">If you want toocreate a VM from a specialized VHD in a storage account, see [Create a VM from a specialized VHD](sa-create-vm-specialized.md).</span></span>

<span data-ttu-id="447b5-107">Este tema incluye el uso de las cuentas de almacenamiento, pero se recomienda a los clientes mover discos administrados de toousing en su lugar.</span><span class="sxs-lookup"><span data-stu-id="447b5-107">This topic covers using storage accounts, but we recommend customers move toousing Managed Disks instead.</span></span> <span data-ttu-id="447b5-108">Para ver un tutorial completo de cómo tooprepare, cargar y crear una nueva máquina virtual mediante discos administrados, vea [crear una nueva máquina virtual desde un tooAzure de disco duro virtual cargado generalizado con discos administrados](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="447b5-108">For a complete walk-through of how tooprepare, upload and create a new VM using managed disks, see [Create a new VM from a generalized VHD uploaded tooAzure using Managed Disks](upload-generalized-managed.md).</span></span>



## <a name="prepare-hello-vm"></a><span data-ttu-id="447b5-109">Preparar Hola VM</span><span class="sxs-lookup"><span data-stu-id="447b5-109">Prepare hello VM</span></span>

<span data-ttu-id="447b5-110">La información personal de la cuenta se elimina de un VHD generalizado mediante Sysprep.</span><span class="sxs-lookup"><span data-stu-id="447b5-110">A generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="447b5-111">Si piensa toouse Hola VHD como una imagen toocreate nuevas máquinas virtuales desde, debe:</span><span class="sxs-lookup"><span data-stu-id="447b5-111">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span>
  
  * <span data-ttu-id="447b5-112">[Preparar una tooAzure de tooupload de disco duro virtual de Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="447b5-112">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> 
  * <span data-ttu-id="447b5-113">Generalice la máquina virtual de hello mediante Sysprep</span><span class="sxs-lookup"><span data-stu-id="447b5-113">Generalize hello virtual machine using Sysprep</span></span>

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a><span data-ttu-id="447b5-114">Generalización de una máquina virtual Windows con Sysprep</span><span class="sxs-lookup"><span data-stu-id="447b5-114">Generalize a Windows virtual machine using Sysprep</span></span>
<span data-ttu-id="447b5-115">Esta sección muestra cómo toogeneralize la máquina virtual de Windows para su uso como una imagen.</span><span class="sxs-lookup"><span data-stu-id="447b5-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="447b5-116">Sysprep quita toda la información de cuenta personal, entre otras cosas y prepara Hola máquina toobe utilizado como una imagen.</span><span class="sxs-lookup"><span data-stu-id="447b5-116">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="447b5-117">Para obtener más información acerca de Sysprep, consulte [cómo tooUse Sysprep: Introducción](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="447b5-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="447b5-118">Asegúrese de que los roles de servidor hello ejecutando en el equipo de hello son compatibles con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="447b5-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="447b5-119">Para más información, consulte [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="447b5-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="447b5-120">Si está ejecutando Sysprep antes de cargar su tooAzure de disco duro virtual para hello primera vez, asegúrese de que tiene [preparado la máquina virtual](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de ejecutar Sysprep.</span><span class="sxs-lookup"><span data-stu-id="447b5-120">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="447b5-121">Inicie sesión en toohello máquina virtual de Windows.</span><span class="sxs-lookup"><span data-stu-id="447b5-121">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="447b5-122">Abra la ventana de símbolo del sistema de hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="447b5-122">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="447b5-123">Cambie el directorio de hello demasiado**%windir%\system32\sysprep**y, a continuación, ejecute `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="447b5-123">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="447b5-124">Hola **herramienta de preparación del sistema** cuadro de diálogo, seleccione **sistema Out-of-Box experiencia inmediata (OOBE)**y asegúrese de que ese hello **generalizar** casilla está activada.</span><span class="sxs-lookup"><span data-stu-id="447b5-124">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="447b5-125">En **Opciones de apagado**, seleccione **Apagar**.</span><span class="sxs-lookup"><span data-stu-id="447b5-125">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="447b5-126">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="447b5-126">Click **OK**.</span></span>
   
    ![Iniciar Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="447b5-128">Cuando Sysprep finalice, se apaga máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="447b5-128">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="447b5-129">No se reinician Hola VM hasta que esté listo cargando tooAzure de disco duro virtual de Hola o crear una imagen de VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="447b5-129">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="447b5-130">Si obtiene reinicia Hola VM accidentalmente, ejecute Sysprep toogeneralize vuelva a.</span><span class="sxs-lookup"><span data-stu-id="447b5-130">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 


## <a name="upload-hello-vhd"></a><span data-ttu-id="447b5-131">Cargar Hola VHD</span><span class="sxs-lookup"><span data-stu-id="447b5-131">Upload hello VHD</span></span>

<span data-ttu-id="447b5-132">Cargar la cuenta de almacenamiento de Azure de hello VHD tooan.</span><span class="sxs-lookup"><span data-stu-id="447b5-132">Upload hello VHD tooan Azure storage account.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="447b5-133">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="447b5-133">Log in tooAzure</span></span>
<span data-ttu-id="447b5-134">Si aún no tiene PowerShell versión 1.4 o posterior instalado, leer [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="447b5-134">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="447b5-135">Abra PowerShell de Azure e inicie sesión tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="447b5-135">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="447b5-136">Abre una ventana emergente para tooenter sus credenciales de cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="447b5-136">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="447b5-137">Obtener identificadores de suscripción de Hola para las suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="447b5-137">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="447b5-138">Conjunto Hola suscripción correcta con el identificador de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="447b5-138">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="447b5-139">Reemplace `<subscriptionID>` con el Id. de Hola de hello corregir la suscripción.</span><span class="sxs-lookup"><span data-stu-id="447b5-139">Replace `<subscriptionID>` with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a><span data-ttu-id="447b5-140">Obtener la cuenta de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="447b5-140">Get hello storage account</span></span>
<span data-ttu-id="447b5-141">Necesita una cuenta de almacenamiento en la imagen de máquina virtual de Azure toostore Hola cargado.</span><span class="sxs-lookup"><span data-stu-id="447b5-141">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="447b5-142">Puede usar una cuenta de almacenamiento existente o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="447b5-142">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="447b5-143">cuentas de almacenamiento disponibles de hello tooshow, escriba:</span><span class="sxs-lookup"><span data-stu-id="447b5-143">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="447b5-144">Si desea que toouse una cuenta de almacenamiento existente, continúe toohello [imagen de máquina virtual de carga hello](#upload-the-vm-vhd-to-your-storage-account) sección.</span><span class="sxs-lookup"><span data-stu-id="447b5-144">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="447b5-145">Si necesita toocreate una cuenta de almacenamiento, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="447b5-145">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="447b5-146">Se necesita el nombre de Hola Hola del grupo de recursos donde se debe crear la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="447b5-146">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="447b5-147">toofind todos los grupos de recursos de Hola que se encuentran en su suscripción, tipo:</span><span class="sxs-lookup"><span data-stu-id="447b5-147">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="447b5-148">toocreate un grupo de recursos denominado **myResourceGroup** Hola **West US** región, escriba:</span><span class="sxs-lookup"><span data-stu-id="447b5-148">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="447b5-149">Crear una cuenta de almacenamiento denominada **mystorageaccount** en este grupo de recursos mediante el uso de hello [AzureRmStorageAccount New](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="447b5-149">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a><span data-ttu-id="447b5-150">Iniciar Hola carga</span><span class="sxs-lookup"><span data-stu-id="447b5-150">Start hello upload</span></span> 

<span data-ttu-id="447b5-151">Hola de uso [AzureRmVhd agregar](/powershell/module/azurerm.compute/add-azurermvhd) contenedor cmdlet tooupload Hola imagen tooa en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="447b5-151">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="447b5-152">En este ejemplo Hola a cargas de archivo **myVHD.vhd** de `"C:\Users\Public\Documents\Virtual hard disks\"` tooa cuenta de almacenamiento denominada **mystorageaccount** en hello **myResourceGroup** grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="447b5-152">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="447b5-153">archivo Hello se colocarán en el contenedor de hello denominado **mycontainer** y nombre de archivo nuevo de hello será **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="447b5-153">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="447b5-154">Si se realiza correctamente, obtendrá una respuesta que busca toothis similar:</span><span class="sxs-lookup"><span data-stu-id="447b5-154">If successful, you get a response that looks similar toothis:</span></span>

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="447b5-155">Dependiendo de la conexión de red y el tamaño de hello del archivo VHD, este comando puede tardar un rato toocomplete.</span><span class="sxs-lookup"><span data-stu-id="447b5-155">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="create-a-new-vm"></a><span data-ttu-id="447b5-156">Creación de una máquina virtual nueva</span><span class="sxs-lookup"><span data-stu-id="447b5-156">Create a new VM</span></span> 

<span data-ttu-id="447b5-157">Ahora puede usar Hola carga VHD toocreate una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="447b5-157">You can now use hello uploaded VHD toocreate a new VM.</span></span> 

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="447b5-158">Hola de conjunto de URI de hello VHD</span><span class="sxs-lookup"><span data-stu-id="447b5-158">Set hello URI of hello VHD</span></span>

<span data-ttu-id="447b5-159">Hola URI para hello toouse de disco duro virtual está en formato de hello: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span><span class="sxs-lookup"><span data-stu-id="447b5-159">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="447b5-160">En este ejemplo Hola VHD denominada **myVHD** está en la cuenta de almacenamiento de hello **mystorageaccount** en el contenedor de hello **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="447b5-160">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="447b5-161">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="447b5-161">Create a virtual network</span></span>
<span data-ttu-id="447b5-162">Crear red virtual de Hola y de las subredes de hello [red virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="447b5-162">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="447b5-163">Crear una subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="447b5-163">Create hello subnet.</span></span> <span data-ttu-id="447b5-164">Hello en el ejemplo siguiente crea una subred denominada **mySubnet** en grupo de recursos de hello **myResourceGroup** con prefijo de dirección de hello **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="447b5-164">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="447b5-165">Crear red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="447b5-165">Create hello virtual network.</span></span> <span data-ttu-id="447b5-166">Hello en el ejemplo siguiente crea una red virtual con el nombre **myVnet** Hola **West US** ubicación con el prefijo de dirección de hello **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="447b5-166">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="447b5-167">Creación de una dirección IP y una interfaz de red</span><span class="sxs-lookup"><span data-stu-id="447b5-167">Create a public IP address and network interface</span></span>
<span data-ttu-id="447b5-168">tooenable la comunicación con la máquina virtual de hello en la red virtual de hello, necesita un [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) y una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="447b5-168">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="447b5-169">Cree una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="447b5-169">Create a public IP address.</span></span> <span data-ttu-id="447b5-170">Este ejemplo crea una dirección IP pública denominada "**myPip**".</span><span class="sxs-lookup"><span data-stu-id="447b5-170">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="447b5-171">Crear NIC de Hola.</span><span class="sxs-lookup"><span data-stu-id="447b5-171">Create hello NIC.</span></span> <span data-ttu-id="447b5-172">Este ejemplo crea una NIC denominada "**myNic**".</span><span class="sxs-lookup"><span data-stu-id="447b5-172">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="447b5-173">Crear grupo de seguridad de red de hello y una regla de RDP</span><span class="sxs-lookup"><span data-stu-id="447b5-173">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="447b5-174">toobe puede toolog en tooyour VM mediante RDP, deberá toohave una regla de seguridad que permite el acceso RDP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="447b5-174">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="447b5-175">Este ejemplo crea un NSG denominado"**myNsg**" que contiene una regla llamada "**myRdpRule**" que permita el tráfico RDP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="447b5-175">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="447b5-176">Para obtener más información acerca de los NSG, consulte [abrir puertos tooa VM en Azure con PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="447b5-176">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="447b5-177">Cree una variable para la red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="447b5-177">Create a variable for hello virtual network</span></span>
<span data-ttu-id="447b5-178">Cree una variable para la red virtual de hello completado.</span><span class="sxs-lookup"><span data-stu-id="447b5-178">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="447b5-179">Crear hello VM</span><span class="sxs-lookup"><span data-stu-id="447b5-179">Create hello VM</span></span>
<span data-ttu-id="447b5-180">Hello siguiente script de PowerShell muestra cómo tooset configuraciones de máquina virtual de Hola y Hola uso carga imagen de máquina virtual como origen de Hola para instalación nueva de Hola.</span><span class="sxs-lookup"><span data-stu-id="447b5-180">hello following PowerShell script shows how tooset up hello virtual machine configurations and use hello uploaded VM image as hello source for hello new installation.</span></span>



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

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="447b5-181">Compruebe que se creó la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="447b5-181">Verify that hello VM was created</span></span>
<span data-ttu-id="447b5-182">Cuando haya finalizado, debería ver Hola recién creado VM hello [portal de Azure](https://portal.azure.com) en **examinar** > **máquinas virtuales**, o mediante Hola siguiente Comandos de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="447b5-182">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="447b5-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="447b5-183">Next steps</span></span>
<span data-ttu-id="447b5-184">toomanage la nueva máquina virtual con PowerShell de Azure, consulte [administrar máquinas virtuales con el Administrador de recursos de Azure y PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="447b5-184">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


