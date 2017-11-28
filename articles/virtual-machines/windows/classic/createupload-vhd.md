---
title: "Creación y carga de una imagen de máquina virtual mediante Powershell | Microsoft Docs"
description: "Aprenda a crear y cargar una imagen de Windows Server generalizada (VHD) mediante el modelo de implementación clásica y Azure Powershell."
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
ms.openlocfilehash: bc75c8cdd98b0ea0fbff6483c0e3c9d4468d3941
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-upload-a-windows-server-vhd-to-azure"></a><span data-ttu-id="9b303-103">Crear y cargar un VHD de Windows Server a Azure</span><span class="sxs-lookup"><span data-stu-id="9b303-103">Create and upload a Windows Server VHD to Azure</span></span>
<span data-ttu-id="9b303-104">En este artículo se muestra cómo puede cargar su propia imagen de VM generalizada como un disco duro virtual (VHD) que podrá utilizar para crear máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9b303-104">This article shows you how to upload your own generalized VM image as a virtual hard disk (VHD) so you can use it to create virtual machines.</span></span> <span data-ttu-id="9b303-105">Para más información sobre discos y VHD en Microsoft Azure, consulte [Acerca de los discos y los discos duros virtuales para máquinas virtuales](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9b303-105">For more details about disks and VHDs in Microsoft Azure, see [About Disks and VHDs for Virtual Machines](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b303-106">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9b303-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9b303-107">En este artículo se trata el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="9b303-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="9b303-108">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="9b303-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="9b303-109">También puede [cargar](../upload-generalized-managed.md) una máquina virtual mediante el modelo Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9b303-109">You can also [upload](../upload-generalized-managed.md) a virtual machine using the Resource Manager model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b303-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9b303-110">Prerequisites</span></span>
<span data-ttu-id="9b303-111">En este artículo se supone que ya dispones de:</span><span class="sxs-lookup"><span data-stu-id="9b303-111">This article assumes you have:</span></span>

* <span data-ttu-id="9b303-112">**Una suscripción a Azure** : si no tiene una, puede [abrir una cuenta de Azure gratis](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="9b303-112">**An Azure subscription** - If you don't have one, you can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="9b303-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)**: tiene el módulo Microsoft Azure PowerShell instalado y configurado para usar su suscripción.</span><span class="sxs-lookup"><span data-stu-id="9b303-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)** - You have the Microsoft Azure PowerShell module installed and configured to use your subscription.</span></span>
* <span data-ttu-id="9b303-114">**Un archivo .VHD** : sistema operativo Windows compatible almacenado en un archivo .vhd y conectado a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9b303-114">**A .VHD file** - supported Windows operating system stored in a .vhd file and attached to a virtual machine.</span></span> <span data-ttu-id="9b303-115">Compruebe si los roles de servidor que se ejecutan en el VHD son compatibles con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="9b303-115">Check to see if the server roles running on the VHD are supported by Sysprep.</span></span> <span data-ttu-id="9b303-116">Para más información, consulte [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)(Compatibilidad de Sysprep con roles de servidor).</span><span class="sxs-lookup"><span data-stu-id="9b303-116">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9b303-117">El formato VHDX no se admite en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9b303-117">The VHDX format is not supported in Microsoft Azure.</span></span> <span data-ttu-id="9b303-118">Puede convertir el disco al formato VHD con el Administrador de Hyper-V o el [cmdlet Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b303-118">You can convert the disk to VHD format using Hyper-V Manager or the [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="9b303-119">Para obtener más información, consulta esta [publicación de blog](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b303-119">For details, see this [blogpost](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span></span>

## <a name="step-1-prep-the-vhd"></a><span data-ttu-id="9b303-120">Paso 1: Preparar el VHD</span><span class="sxs-lookup"><span data-stu-id="9b303-120">Step 1: Prep the VHD</span></span>
<span data-ttu-id="9b303-121">Antes de cargar el VHD en Azure, tiene que generalizarse mediante la herramienta Sysprep.</span><span class="sxs-lookup"><span data-stu-id="9b303-121">Before you upload the VHD to Azure, it needs to be generalized by using the Sysprep tool.</span></span> <span data-ttu-id="9b303-122">Esto prepara el VHD para usarlo como una imagen.</span><span class="sxs-lookup"><span data-stu-id="9b303-122">This prepares the VHD to be used as an image.</span></span> <span data-ttu-id="9b303-123">Para obtener más información sobre Sysprep, vea [Uso de Sysprep: Introducción](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b303-123">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> <span data-ttu-id="9b303-124">Cree una copia de seguridad de la VM antes de ejecutar Sysprep.</span><span class="sxs-lookup"><span data-stu-id="9b303-124">Back up the VM before running Sysprep.</span></span>

<span data-ttu-id="9b303-125">Desde la máquina virtual en la que se instaló el sistema operativo, realice el procedimiento siguiente:</span><span class="sxs-lookup"><span data-stu-id="9b303-125">From the virtual machine that the operating system was installed to, complete the following procedure:</span></span>

1. <span data-ttu-id="9b303-126">Inicie sesión en el sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="9b303-126">Sign in to the operating system.</span></span>
2. <span data-ttu-id="9b303-127">Abra una ventana del símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="9b303-127">Open a command prompt window as an administrator.</span></span> <span data-ttu-id="9b303-128">Cambie el directorio a **%windir%\system32\sysprep** y, después, ejecute `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="9b303-128">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>

    ![Abrir una ventana de símbolo del sistema](./media/createupload-vhd/sysprep_commandprompt.png)
3. <span data-ttu-id="9b303-130">Aparecerá el cuadro de diálogo **Herramienta de preparación del sistema** .</span><span class="sxs-lookup"><span data-stu-id="9b303-130">The **System Preparation Tool** dialog box appears.</span></span>

   ![Iniciar Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. <span data-ttu-id="9b303-132">En la **Herramienta de preparación del sistema**, seleccione **Iniciar la configuración rápida (OOBE) del sistema** y asegúrese de que la casilla **Generalizar** está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="9b303-132">In the **System Preparation Tool**, select **Enter System Out of Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span>
5. <span data-ttu-id="9b303-133">En **Opciones de apagado**, seleccione **Apagar**.</span><span class="sxs-lookup"><span data-stu-id="9b303-133">In **Shutdown Options**, select **Shutdown**.</span></span>
6. <span data-ttu-id="9b303-134">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9b303-134">Click **OK**.</span></span>

## <a name="step-2-create-a-storage-account-and-a-container"></a><span data-ttu-id="9b303-135">Paso 2: Crear una cuenta de almacenamiento y un contenedor</span><span class="sxs-lookup"><span data-stu-id="9b303-135">Step 2: Create a storage account and a container</span></span>
<span data-ttu-id="9b303-136">Necesitas una cuenta de almacenamiento de Azure para tener un sitio para cargar el archivo .vhd.</span><span class="sxs-lookup"><span data-stu-id="9b303-136">You need a storage account in Azure so you have a place to upload the .vhd file.</span></span> <span data-ttu-id="9b303-137">Este paso te muestra cómo crear una cuenta u obtener la información que necesitas de una cuenta existente.</span><span class="sxs-lookup"><span data-stu-id="9b303-137">This step shows you how to create an account, or get the info you need from an existing account.</span></span> <span data-ttu-id="9b303-138">Reemplace las variables entre &lsaquo; corchetes &rsaquo; por su propia información.</span><span class="sxs-lookup"><span data-stu-id="9b303-138">Replace the variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

1. <span data-ttu-id="9b303-139">Inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="9b303-139">Login</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="9b303-140">Establezca su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="9b303-140">Set your Azure subscription.</span></span>

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. <span data-ttu-id="9b303-141">Cree una cuenta de almacenamiento nueva.</span><span class="sxs-lookup"><span data-stu-id="9b303-141">Create a new storage account.</span></span> <span data-ttu-id="9b303-142">El nombre de la cuenta de almacenamiento debe ser único y debe tener entre 3 y 24 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9b303-142">The name of the storage account should be unique, 3-24 characters.</span></span> <span data-ttu-id="9b303-143">El nombre puede ser cualquier combinación de letras y números.</span><span class="sxs-lookup"><span data-stu-id="9b303-143">The name can be any combination of letters and numbers.</span></span> <span data-ttu-id="9b303-144">También necesita especificar una ubicación como "Este de EE. UU. "</span><span class="sxs-lookup"><span data-stu-id="9b303-144">You also need to specify a location like "East US"</span></span>

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. <span data-ttu-id="9b303-145">Establezca la nueva cuenta de almacenamiento como la predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9b303-145">Set the new storage account as the default.</span></span>

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. <span data-ttu-id="9b303-146">Cree un contenedor nuevo.</span><span class="sxs-lookup"><span data-stu-id="9b303-146">Create a new container.</span></span>

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-the-vhd-file"></a><span data-ttu-id="9b303-147">Paso 3: Cargar el archivo .vhd</span><span class="sxs-lookup"><span data-stu-id="9b303-147">Step 3: Upload the .vhd file</span></span>
<span data-ttu-id="9b303-148">Use [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) para cargar el VHD.</span><span class="sxs-lookup"><span data-stu-id="9b303-148">Use the [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) to upload the VHD.</span></span>

<span data-ttu-id="9b303-149">Desde la ventana de Azure PowerShell que usó en el paso anterior, escriba el siguiente comando y reemplace las variables entre &lsaquo; corchetes &rsaquo; por su propia información.</span><span class="sxs-lookup"><span data-stu-id="9b303-149">From the Azure PowerShell window you used in the previous step, type the following command and replace the variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-the-image-to-your-list-of-custom-images"></a><span data-ttu-id="9b303-150">Paso 4: Agregar la imagen a la lista de imágenes personalizadas</span><span class="sxs-lookup"><span data-stu-id="9b303-150">Step 4: Add the image to your list of custom images</span></span>
<span data-ttu-id="9b303-151">Use el cmdlet [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) para agregar la imagen a la lista de imágenes personalizadas.</span><span class="sxs-lookup"><span data-stu-id="9b303-151">Use the [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet to add the image to the list of your custom images.</span></span>

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a><span data-ttu-id="9b303-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b303-152">Next steps</span></span>
<span data-ttu-id="9b303-153">Ahora puede [crear una máquina virtual personalizada](createportal.md) mediante la imagen que cargó.</span><span class="sxs-lookup"><span data-stu-id="9b303-153">You can now [create a custom VM](createportal.md) using the image you uploaded.</span></span>
