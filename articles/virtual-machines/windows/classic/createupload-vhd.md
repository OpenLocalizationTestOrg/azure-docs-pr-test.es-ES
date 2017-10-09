---
title: "las imágenes aaaCreate y carga una máquina virtual mediante Powershell | Documentos de Microsoft"
description: "Obtenga información acerca de toocreate y cargar una imagen generalizada de Windows Server (VHD) mediante el modelo de implementación clásica de Hola y Powershell de Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 093b57c9157cea5f348c8ba02b5700c917adbcdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a><span data-ttu-id="6b07a-103">Crear y cargar un VHD de Windows Server tooAzure</span><span class="sxs-lookup"><span data-stu-id="6b07a-103">Create and upload a Windows Server VHD tooAzure</span></span>
<span data-ttu-id="6b07a-104">Este artículo muestra cómo tooupload su propio generalizada imágenes de máquina virtual como un disco duro virtual (VHD) por lo que puede usar máquinas virtuales de toocreate.</span><span class="sxs-lookup"><span data-stu-id="6b07a-104">This article shows you how tooupload your own generalized VM image as a virtual hard disk (VHD) so you can use it toocreate virtual machines.</span></span> <span data-ttu-id="6b07a-105">Para más información sobre discos y VHD en Microsoft Azure, consulte [Acerca de los discos y los discos duros virtuales para máquinas virtuales](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6b07a-105">For more details about disks and VHDs in Microsoft Azure, see [About Disks and VHDs for Virtual Machines](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b07a-106">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6b07a-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6b07a-107">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="6b07a-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="6b07a-108">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b07a-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="6b07a-109">También puede [cargar](../upload-generalized-managed.md) una máquina virtual mediante el modelo de administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b07a-109">You can also [upload](../upload-generalized-managed.md) a virtual machine using hello Resource Manager model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b07a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6b07a-110">Prerequisites</span></span>
<span data-ttu-id="6b07a-111">En este artículo se supone que ya dispones de:</span><span class="sxs-lookup"><span data-stu-id="6b07a-111">This article assumes you have:</span></span>

* <span data-ttu-id="6b07a-112">**Una suscripción a Azure** : si no tiene una, puede [abrir una cuenta de Azure gratis](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="6b07a-112">**An Azure subscription** - If you don't have one, you can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="6b07a-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)**  -tienen Hola Microsoft Azure PowerShell módulo instalado y configurado toouse su suscripción.</span><span class="sxs-lookup"><span data-stu-id="6b07a-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)** - You have hello Microsoft Azure PowerShell module installed and configured toouse your subscription.</span></span>
* <span data-ttu-id="6b07a-114">**UN ARCHIVO. Archivo de disco duro virtual** : almacenado en un archivo .vhd y la máquina virtual de tooa adjunto de sistema operativo de Windows compatibles.</span><span class="sxs-lookup"><span data-stu-id="6b07a-114">**A .VHD file** - supported Windows operating system stored in a .vhd file and attached tooa virtual machine.</span></span> <span data-ttu-id="6b07a-115">Compruebe toosee si los roles de servidor hello con hello VHD son compatibles con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="6b07a-115">Check toosee if hello server roles running on hello VHD are supported by Sysprep.</span></span> <span data-ttu-id="6b07a-116">Para más información, consulte [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)(Compatibilidad de Sysprep con roles de servidor).</span><span class="sxs-lookup"><span data-stu-id="6b07a-116">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6b07a-117">no se admite el formato VHDX Hello en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6b07a-117">hello VHDX format is not supported in Microsoft Azure.</span></span> <span data-ttu-id="6b07a-118">Puede convertir el formato de tooVHD de disco hello mediante el Administrador de Hyper-V o hello [cmdlet Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b07a-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="6b07a-119">Para obtener más información, consulta esta [publicación de blog](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b07a-119">For details, see this [blogpost](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span></span>

## <a name="step-1-prep-hello-vhd"></a><span data-ttu-id="6b07a-120">Paso 1: Preparar el disco duro virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="6b07a-120">Step 1: Prep hello VHD</span></span>
<span data-ttu-id="6b07a-121">Antes de cargar hello tooAzure de disco duro virtual, debe toobe generalizado con la herramienta Sysprep de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b07a-121">Before you upload hello VHD tooAzure, it needs toobe generalized by using hello Sysprep tool.</span></span> <span data-ttu-id="6b07a-122">Esto prepara Hola VHD toobe utilizado como una imagen.</span><span class="sxs-lookup"><span data-stu-id="6b07a-122">This prepares hello VHD toobe used as an image.</span></span> <span data-ttu-id="6b07a-123">Para obtener más información acerca de Sysprep, consulte [cómo tooUse Sysprep: Introducción](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b07a-123">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> <span data-ttu-id="6b07a-124">Respaldar Hola VM antes de ejecutar Sysprep.</span><span class="sxs-lookup"><span data-stu-id="6b07a-124">Back up hello VM before running Sysprep.</span></span>

<span data-ttu-id="6b07a-125">En la máquina virtual Hola Hola sistema operativo se instaló para completar Hola siguiendo el procedimiento:</span><span class="sxs-lookup"><span data-stu-id="6b07a-125">From hello virtual machine that hello operating system was installed to, complete hello following procedure:</span></span>

1. <span data-ttu-id="6b07a-126">Inicie sesión en el sistema operativo de toohello.</span><span class="sxs-lookup"><span data-stu-id="6b07a-126">Sign in toohello operating system.</span></span>
2. <span data-ttu-id="6b07a-127">Abra una ventana del símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="6b07a-127">Open a command prompt window as an administrator.</span></span> <span data-ttu-id="6b07a-128">Cambie el directorio de hello demasiado**%windir%\system32\sysprep**y, a continuación, ejecute `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="6b07a-128">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>

    ![Abrir una ventana de símbolo del sistema](./media/createupload-vhd/sysprep_commandprompt.png)
3. <span data-ttu-id="6b07a-130">Hola **herramienta de preparación del sistema** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6b07a-130">hello **System Preparation Tool** dialog box appears.</span></span>

   ![Iniciar Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. <span data-ttu-id="6b07a-132">Hola **herramienta de preparación del sistema**, seleccione **escriba sistema fuera de cuadro de experiencia de configuración rápida (OOBE)** y asegúrese de que **generalizar** está activada.</span><span class="sxs-lookup"><span data-stu-id="6b07a-132">In hello **System Preparation Tool**, select **Enter System Out of Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span>
5. <span data-ttu-id="6b07a-133">En **Opciones de apagado**, seleccione **Apagar**.</span><span class="sxs-lookup"><span data-stu-id="6b07a-133">In **Shutdown Options**, select **Shutdown**.</span></span>
6. <span data-ttu-id="6b07a-134">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6b07a-134">Click **OK**.</span></span>

## <a name="step-2-create-a-storage-account-and-a-container"></a><span data-ttu-id="6b07a-135">Paso 2: Crear una cuenta de almacenamiento y un contenedor</span><span class="sxs-lookup"><span data-stu-id="6b07a-135">Step 2: Create a storage account and a container</span></span>
<span data-ttu-id="6b07a-136">Necesita una cuenta de almacenamiento de Azure para tener un archivo .vhd de lugar tooupload Hola.</span><span class="sxs-lookup"><span data-stu-id="6b07a-136">You need a storage account in Azure so you have a place tooupload hello .vhd file.</span></span> <span data-ttu-id="6b07a-137">Este paso muestra cómo toocreate una cuenta o get Hola información que necesita de una cuenta existente.</span><span class="sxs-lookup"><span data-stu-id="6b07a-137">This step shows you how toocreate an account, or get hello info you need from an existing account.</span></span> <span data-ttu-id="6b07a-138">Reemplace las variables de hello en &lsaquo; corchetes &rsaquo; con su propia información.</span><span class="sxs-lookup"><span data-stu-id="6b07a-138">Replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

1. <span data-ttu-id="6b07a-139">Inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="6b07a-139">Login</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="6b07a-140">Establezca su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="6b07a-140">Set your Azure subscription.</span></span>

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. <span data-ttu-id="6b07a-141">Cree una cuenta de almacenamiento nueva.</span><span class="sxs-lookup"><span data-stu-id="6b07a-141">Create a new storage account.</span></span> <span data-ttu-id="6b07a-142">Hola nombre de cuenta de almacenamiento de hello debe ser único, 3 y 24 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6b07a-142">hello name of hello storage account should be unique, 3-24 characters.</span></span> <span data-ttu-id="6b07a-143">nombre de Hello puede ser cualquier combinación de letras y números.</span><span class="sxs-lookup"><span data-stu-id="6b07a-143">hello name can be any combination of letters and numbers.</span></span> <span data-ttu-id="6b07a-144">También debe toospecify una ubicación como "Este nosotros"</span><span class="sxs-lookup"><span data-stu-id="6b07a-144">You also need toospecify a location like "East US"</span></span>

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. <span data-ttu-id="6b07a-145">Predeterminar nueva cuenta de almacenamiento Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="6b07a-145">Set hello new storage account as hello default.</span></span>

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. <span data-ttu-id="6b07a-146">Cree un contenedor nuevo.</span><span class="sxs-lookup"><span data-stu-id="6b07a-146">Create a new container.</span></span>

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a><span data-ttu-id="6b07a-147">Paso 3: Cargar archivo .vhd de hello</span><span class="sxs-lookup"><span data-stu-id="6b07a-147">Step 3: Upload hello .vhd file</span></span>
<span data-ttu-id="6b07a-148">Hola de uso [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) hello tooupload disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="6b07a-148">Use hello [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello VHD.</span></span>

<span data-ttu-id="6b07a-149">Desde la ventana de PowerShell de Azure de hello utilizada en el paso anterior de hello, escriba lo siguiente Hola comando y reemplace las variables de hello en &lsaquo; corchetes &rsaquo; con su propia información.</span><span class="sxs-lookup"><span data-stu-id="6b07a-149">From hello Azure PowerShell window you used in hello previous step, type hello following command and replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a><span data-ttu-id="6b07a-150">Paso 4: Agregar lista de hello imágenes tooyour de imágenes personalizadas</span><span class="sxs-lookup"><span data-stu-id="6b07a-150">Step 4: Add hello image tooyour list of custom images</span></span>
<span data-ttu-id="6b07a-151">Hola de uso [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) lista cmdlet tooadd Hola imagen toohello de sus imágenes personalizadas.</span><span class="sxs-lookup"><span data-stu-id="6b07a-151">Use hello [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet tooadd hello image toohello list of your custom images.</span></span>

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a><span data-ttu-id="6b07a-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6b07a-152">Next steps</span></span>
<span data-ttu-id="6b07a-153">Ahora puede [crear una máquina virtual personalizada](createportal.md) utilizando hello de la imagen que ha cargado.</span><span class="sxs-lookup"><span data-stu-id="6b07a-153">You can now [create a custom VM](createportal.md) using hello image you uploaded.</span></span>
