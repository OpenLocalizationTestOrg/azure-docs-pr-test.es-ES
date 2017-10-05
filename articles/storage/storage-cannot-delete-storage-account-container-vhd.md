---
title: "Solución de problemas de eliminación de cuentas, contenedores o discos duros virtuales de Azure Storage en una implementación clásica | Microsoft Docs"
description: "Solución de problemas de eliminación de cuentas de almacenamiento de Azure, contenedores o discos duros virtuales"
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 9f3e824414ad6c1a0aba98a3d549ee63ddc7272f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a><span data-ttu-id="3b2ac-103">Solución de problemas de eliminación de cuentas de almacenamiento de Azure, contenedores o discos duros virtuales</span><span class="sxs-lookup"><span data-stu-id="3b2ac-103">Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment</span></span>
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

<span data-ttu-id="3b2ac-104">Es posible que al intentar eliminar la cuenta de almacenamiento de Azure, un contenedor o un disco duro virtual en [Azure Portal](https://portal.azure.com/) o el [Portal de Azure clásico](https://manage.windowsazure.com/) reciba errores.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-104">You might receive errors when you try to delete the Azure storage account, container, or VHD in the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="3b2ac-105">Los problemas pueden deberse a las siguientes circunstancias:</span><span class="sxs-lookup"><span data-stu-id="3b2ac-105">The issues can be caused by the following circumstances:</span></span>

* <span data-ttu-id="3b2ac-106">Al eliminar una VM, el disco y el disco duro virtual no se eliminan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-106">When you delete a VM, the disk and VHD are not automatically deleted.</span></span> <span data-ttu-id="3b2ac-107">Este podría ser el motivo del error en la eliminación de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-107">That might be the reason for failure on storage account deletion.</span></span> <span data-ttu-id="3b2ac-108">No eliminamos el disco; por tanto, puede usarlo para montar otra máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-108">We don't delete the disk so that you can use the disk to mount another VM.</span></span>
* <span data-ttu-id="3b2ac-109">Sigue habiendo una concesión para un disco o el blob asociado a él.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-109">There is still a lease on a disk or the blob that's associated with the disk.</span></span>
* <span data-ttu-id="3b2ac-110">Sigue siendo una imagen de máquina virtual que está usando una cuenta de almacenamiento, un contenedor o un blob.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-110">There is still a VM image that is using a blob, container, or storage account.</span></span>

<span data-ttu-id="3b2ac-111">Si su problema con Azure no se trata en este artículo, visite los foros de Azure en [MSDN y Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="3b2ac-111">If your Azure issue is not addressed in this article, visit the Azure forums on [MSDN and the Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="3b2ac-112">Puede publicar su problema en ellos o en @AzureSupport en Twitter.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-112">You can post your issue on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="3b2ac-113">También puede presentar una solicitud de soporte técnico de Azure; para ello seleccione **Obtener soporte técnico** en el sitio de [soporte técnico de Azure](https://azure.microsoft.com/support/options/) .</span><span class="sxs-lookup"><span data-stu-id="3b2ac-113">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="3b2ac-114">Síntomas</span><span class="sxs-lookup"><span data-stu-id="3b2ac-114">Symptoms</span></span>
<span data-ttu-id="3b2ac-115">La sección siguiente muestra los errores comunes que puede recibir al intentar eliminar las cuentas de almacenamiento de Azure, los contenedores o los discos duros virtuales.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-115">The following section lists common errors that you might receive when you try to delete the Azure storage accounts, containers, or VHDs.</span></span>

### <a name="scenario-1-unable-to-delete-a-storage-account"></a><span data-ttu-id="3b2ac-116">Escenario 1: No se puede eliminar una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="3b2ac-116">Scenario 1: Unable to delete a storage account</span></span>
<span data-ttu-id="3b2ac-117">Cuando se desplaza a la cuenta clásica de almacenamiento en [Azure Portal](https://portal.azure.com/) y selecciona **Eliminar**, puede que vea una lista de objetos que impiden la eliminación de la cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="3b2ac-117">When you navigate to the classic storage account in the [Azure portal](https://portal.azure.com/) and select **Delete**, you may be presented with a list of objects that are preventing deletion of the storage account:</span></span>

  ![Imagen de error al eliminar la cuenta de Almacenamiento](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

<span data-ttu-id="3b2ac-119">Cuando de desplaza a la cuenta de almacenamiento en [Portal de Azure clásico](https://manage.windowsazure.com/) y selecciona **Eliminar**, puede que vea uno de los mensajes de error siguientes:</span><span class="sxs-lookup"><span data-stu-id="3b2ac-119">When you navigate to the storage account in the [Azure classic portal](https://manage.windowsazure.com/) and select **Delete**, you might see one of the following errors:</span></span>

- <span data-ttu-id="3b2ac-120">*La cuenta de almacenamiento StorageAccountName contiene imágenes de máquina virtual. Asegúrese de que estas imágenes de máquina virtual se quiten antes de eliminar esta cuenta de almacenamiento*.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-120">*Storage account StorageAccountName contains VM Images. Ensure these VM Images are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="3b2ac-121">*Error al eliminar la cuenta de almacenamiento <nombre-de-cuenta-de-almacenamiento-de-vm>. No se puede eliminar la cuenta de almacenamiento <nombre-de-cuenta-de-almacenamiento-de-vm>: 'La cuenta de almacenamiento <nombre-de-cuenta-de-almacenamiento-de-vm> tiene algunas imágenes o discos activos. Controle que se quiten las imágenes y los discos antes de eliminar esta cuenta de almacenamiento.'.*</span><span class="sxs-lookup"><span data-stu-id="3b2ac-121">*Failed to delete storage account <vm-storage-account-name>. Unable to delete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.*</span></span>

- <span data-ttu-id="3b2ac-122">*La cuenta de almacenamiento <nombre-de-cuenta-de-almacenamiento-de-vm> tiene algunas imágenes o discos activos; por ejemplo, xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Controle que se quiten las imágenes y los discos antes de eliminar esta cuenta de almacenamiento.*</span><span class="sxs-lookup"><span data-stu-id="3b2ac-122">*Storage account <vm-storage-account-name> has some active image(s) and/or disk(s), e.g. xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Ensure these image(s) and/or disk(s) are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="3b2ac-123">*La cuenta de almacenamiento <nombre-de-cuenta-de-almacenamiento> tiene 1 contenedor que tiene artefactos de imagen o disco activos. Compruebe que estos artefactos se quitan del repositorio de imágenes antes de eliminar esta cuenta de almacenamiento*.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-123">*Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account*.</span></span>

- <span data-ttu-id="3b2ac-124">*Error en el envío. La cuenta de almacenamiento <nombre-de-cuenta-de-almacenamiento-de-vm> tiene 1 contenedor que tiene artefactos de imagen o disco activos. Compruebe que estos artefactos se quitan del repositorio de imágenes antes de eliminar esta cuenta de almacenamiento. Cuando se intenta eliminar una cuenta de almacenamiento y todavía hay discos activos asociados a ella, verá un mensaje que le indica que hay discos activos que deben eliminarse*.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-124">*Submit Failed Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account. When you attempt to delete a storage account and there are still active disks associated with it, you will see a message telling you there are active disks that need to be deleted*.</span></span>

### <a name="scenario-2-unable-to-delete-a-container"></a><span data-ttu-id="3b2ac-125">Escenario 2: No se puede eliminar un contenedor</span><span class="sxs-lookup"><span data-stu-id="3b2ac-125">Scenario 2: Unable to delete a container</span></span>
<span data-ttu-id="3b2ac-126">Al intentar eliminar el contenedor de almacenamiento, podría ver el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="3b2ac-126">When you try to delete the storage container, you might see the following error:</span></span>

<span data-ttu-id="3b2ac-127">*No se pudo eliminar el contenedor de almacenamiento <container name>. Error: 'Actualmente hay una concesión en el contenedor y no se especificó ningún identificador de concesión en la solicitud*.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-127">*Failed to delete storage container <container name>. Error: 'There is currently a lease on the container and no lease ID was specified in the request*.</span></span>

<span data-ttu-id="3b2ac-128">o</span><span class="sxs-lookup"><span data-stu-id="3b2ac-128">Or</span></span>

<span data-ttu-id="3b2ac-129">*Los siguientes discos de máquina virtual usan blobs en este contenedor, por lo que este no puede eliminarse: VirtualMachineDiskName1, VirtualMachineDiskName2, etc.*</span><span class="sxs-lookup"><span data-stu-id="3b2ac-129">*The following virtual machine disks use blobs in this container, so the container cannot be deleted: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span></span>

### <a name="scenario-3-unable-to-delete-a-vhd"></a><span data-ttu-id="3b2ac-130">Escenario 3: No se puede eliminar un VHD</span><span class="sxs-lookup"><span data-stu-id="3b2ac-130">Scenario 3: Unable to delete a VHD</span></span>
<span data-ttu-id="3b2ac-131">Después de eliminar una VM e intentar eliminar después los blobs de los discos duros virtuales asociados, podría recibir el mensaje siguiente:</span><span class="sxs-lookup"><span data-stu-id="3b2ac-131">After you delete a VM and then try to delete the blobs for the associated VHDs, you might receive the following message:</span></span>

<span data-ttu-id="3b2ac-132">*Error al eliminar el blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: 'Actualmente hay una concesión en el blob y no se especificó ningún identificador de concesión en la solicitud.*</span><span class="sxs-lookup"><span data-stu-id="3b2ac-132">*Failed to delete blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: 'There is currently a lease on the blob and no lease ID was specified in the request.*</span></span>

<span data-ttu-id="3b2ac-133">o</span><span class="sxs-lookup"><span data-stu-id="3b2ac-133">Or</span></span>

<span data-ttu-id="3b2ac-134">*El blob "BlobName.vhd" se está usando como disco de máquina virtual "VirtualMachineDiskName", por lo que no se puede eliminar.*</span><span class="sxs-lookup"><span data-stu-id="3b2ac-134">*Blob 'BlobName.vhd' is in use as virtual machine disk 'VirtualMachineDiskName', so the blob cannot be deleted.*</span></span>

## <a name="solution"></a><span data-ttu-id="3b2ac-135">Solución</span><span class="sxs-lookup"><span data-stu-id="3b2ac-135">Solution</span></span>
<span data-ttu-id="3b2ac-136">Para resolver los problemas más comunes, pruebe el siguiente método:</span><span class="sxs-lookup"><span data-stu-id="3b2ac-136">To resolve the most common issues, try the following method:</span></span>

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-the-storage-account-container-or-vhd"></a><span data-ttu-id="3b2ac-137">Paso 1: Eliminar los discos que impiden la eliminación de la cuenta de almacenamiento, el contenedor o el VHD</span><span class="sxs-lookup"><span data-stu-id="3b2ac-137">Step 1: Delete any disks that are preventing deletion of the storage account, container, or VHD</span></span>
1. <span data-ttu-id="3b2ac-138">Cambie al [Portal de Azure clásico](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="3b2ac-138">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="3b2ac-139">Seleccione **MÁQUINA VIRTUAL** > **DISCOS**.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-139">Select **VIRTUAL MACHINE** > **DISKS**.</span></span>

    ![Imagen de discos en máquinas virtuales en el Portal de Azure clásico.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. <span data-ttu-id="3b2ac-141">Busque los discos asociados a la cuenta de almacenamiento, contenedor o disco duro virtual que quiere eliminar.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-141">Locate the disks that are associated with the storage account, container, or VHD that you want to delete.</span></span> <span data-ttu-id="3b2ac-142">Cuando compruebe la ubicación del disco, encontrará la cuenta de almacenamiento asociada, el contenedor y el disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-142">When you check the location of the disk, you will find the associated storage account, container, or VHD.</span></span>

    ![Imagen que muestra la información de ubicación de los discos en el Portal de Azure clásico](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. <span data-ttu-id="3b2ac-144">Elimine los discos mediante uno de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3b2ac-144">Delete the disks by using one of the following methods:</span></span>

  - <span data-ttu-id="3b2ac-145">Si no hay ninguna máquina virtual en el campo **Conectado a** del disco y, después, elimine los discos directamente.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-145">If  there is no VM listed on the **Attached To** field of the disk, you can delete the disk directly.</span></span>

  - <span data-ttu-id="3b2ac-146">Si se trata de un disco de datos, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3b2ac-146">If the disk is a data disk, follow these steps:</span></span>

    1. <span data-ttu-id="3b2ac-147">Compruebe el nombre de la máquina virtual al que está conectado el disco.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-147">Check the name of the VM that the disk is attached to.</span></span>
    2. <span data-ttu-id="3b2ac-148">Vaya a **Máquinas virtuales** > **Instancias** y, luego, busque la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-148">Go to **Virtual Machines** > **Instances**, and then locate the VM.</span></span>
    3. <span data-ttu-id="3b2ac-149">Confirme que no hay ningún recurso usando activamente el disco.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-149">Make sure that nothing is actively using the disk.</span></span>
    4. <span data-ttu-id="3b2ac-150">Seleccione **Desconectar disco** en la parte inferior del portal para desconectar el disco.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-150">Select **Detach Disk** at the bottom of the portal to detach the disk.</span></span>
    5. <span data-ttu-id="3b2ac-151">Vaya a **Máquinas virtuales** > **Discos** y espere a que el campo **Conectado a** se quede vacío.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-151">Go to **Virtual Machines** > **Disks**, and wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="3b2ac-152">Esto indica que el disco se ha desconectado correctamente de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-152">This indicates the disk has successfully detached from the VM.</span></span>
    6. <span data-ttu-id="3b2ac-153">Seleccione **Eliminar** en la parte inferior de **Máquinas virtuales** > **Discos** para eliminar el disco.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-153">Select **Delete** at the bottom of **Virtual Machines** > **Disks** to delete the disk.</span></span>

  - <span data-ttu-id="3b2ac-154">Si se trata de un disco del sistema operativo (el campo **Contiene SO** tiene un valor de Windows) y se conecta a una máquina virtual, siga estos pasos para eliminar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-154">If the disk is an OS disk (the **Contains OS** field has a value like Windows) and attached to a VM, follow these steps to delete the VM.</span></span> <span data-ttu-id="3b2ac-155">No se puede desconectar el disco del sistema operativo, por lo que hay que eliminar la máquina virtual para liberar la concesión.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-155">The OS disk cannot be detached, so we have to delete the VM to release the lease.</span></span>

    1. <span data-ttu-id="3b2ac-156">Compruebe el nombre de la máquina virtual a la que está conectado el disco de datos.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-156">Check the name of the Virtual Machine the Data Disk is attached to.</span></span>  
    2. <span data-ttu-id="3b2ac-157">Vaya a **Máquinas virtuales** > **Instancias** y, luego, seleccione la máquina virtual a la que está conectado el disco.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-157">Go to **Virtual Machines** > **Instances**, and then select the VM that the disk is attached to.</span></span>
    3. <span data-ttu-id="3b2ac-158">Asegúrese de que no haya nada usando activamente la máquina virtual y de que ya no la necesite.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-158">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
    4. <span data-ttu-id="3b2ac-159">Seleccione la máquina virtual a la que está conectado el disco y, luego, haga clic en **Eliminar** > **Eliminar los discos conectados**.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-159">Select the VM the disk is attached to, then select **Delete** > **Delete the attached disks**.</span></span>
    5. <span data-ttu-id="3b2ac-160">Vaya a **Máquinas virtuales** > **Discos** y espere a que el disco desaparezca.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-160">Go to **Virtual Machines** > **Disks**, and wait for the disk to disappear.</span></span>  <span data-ttu-id="3b2ac-161">Puede tardar unos minutos y es posible que tenga que actualizar la página.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-161">It may take a few minutes for this to occur, and you may need to refresh the page.</span></span>
    6. <span data-ttu-id="3b2ac-162">Si el disco no desaparece, espere a que el campo **Conectado a** se quede vacío.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-162">If the disk does not disappear, wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="3b2ac-163">Esto indica que el disco se ha desconectado correctamente de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-163">This indicates the disk has fully detached from the VM.</span></span>  <span data-ttu-id="3b2ac-164">Después, seleccione el disco y haga clic en la opción **Eliminar** de la parte inferior de la página para eliminar el disco.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-164">Then, select the disk, and select **Delete** at the bottom of the page to delete the disk.</span></span>


   > [!NOTE]
   > <span data-ttu-id="3b2ac-165">Si un disco está conectado a una VM, no podrá eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-165">If a disk is attached to a VM, you will not be able to delete it.</span></span> <span data-ttu-id="3b2ac-166">Los discos se desconectan de una máquina virtual eliminada de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-166">Disks are detached from a deleted VM asynchronously.</span></span> <span data-ttu-id="3b2ac-167">Este campo puede tardar unos minutos en borrarse después de eliminar la VM.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-167">It might take a few minutes after the VM is deleted for this field to clear up.</span></span>
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-the-storage-account-or-container"></a><span data-ttu-id="3b2ac-168">Paso 2: Eliminación de las imágenes de máquina virtual que impiden la eliminación de la cuenta de almacenamiento o el contenedor</span><span class="sxs-lookup"><span data-stu-id="3b2ac-168">Step 2: Delete any VM Images that are preventing deletion of the storage account or container</span></span>
1. <span data-ttu-id="3b2ac-169">Cambie al [Portal de Azure clásico](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="3b2ac-169">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="3b2ac-170">Seleccione **MÁQUINA VIRTUAL** > **IMÁGENES** y luego elimine las imágenes asociadas con la cuenta de almacenamiento, el contenedor o el disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-170">Select **VIRTUAL MACHINE** > **IMAGES**, and then delete the images that are associated with the storage account, container, or VHD.</span></span>

    <span data-ttu-id="3b2ac-171">Después, trate de eliminar otra vez la cuenta de almacenamiento, contenedor o disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-171">After that, try to delete the storage account, container, or VHD again.</span></span>

> [!WARNING]
> <span data-ttu-id="3b2ac-172">Asegúrese de hacer una copia de seguridad de cualquier contenido que desee guardar antes de eliminar la cuenta.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-172">Be sure to back up anything you want to save before you delete the account.</span></span> <span data-ttu-id="3b2ac-173">La eliminación de un VHD, blob, tabla, cola o archivo tiene carácter permanente una vez realizada.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-173">Once you delete a VHD, blob, table, queue, or file, it is permanently deleted.</span></span> <span data-ttu-id="3b2ac-174">Asegúrese de que el recurso no está en uso.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-174">Ensure that the resource is not in use.</span></span>
>
>

## <a name="about-the-stopped-deallocated-status"></a><span data-ttu-id="3b2ac-175">Acerca del estado Detenido (desasignado)</span><span class="sxs-lookup"><span data-stu-id="3b2ac-175">About the Stopped (deallocated) status</span></span>
<span data-ttu-id="3b2ac-176">Las VM que se crearon en el modelo de implementación clásica y que se han conservado tendrán el estado **Detenido (desasignado)** tanto en [Azure Portal](https://portal.azure.com/) como en el [Portal de Azure clásico](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="3b2ac-176">VMs that were created in the classic deployment model and that have been retained will have the **Stopped (deallocated)** status on either the [Azure portal](https://portal.azure.com/) or [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="3b2ac-177">**Portal de Azure clásico**:</span><span class="sxs-lookup"><span data-stu-id="3b2ac-177">**Azure classic portal**:</span></span>

![Estado Detenido (desasignado) de VM en el Portal de Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

<span data-ttu-id="3b2ac-179">**Portal de Azure**:</span><span class="sxs-lookup"><span data-stu-id="3b2ac-179">**Azure portal**:</span></span>

![Estado Detenido (desasignado) de VM en el Portal de Azure clásico.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

<span data-ttu-id="3b2ac-181">Un estado "Detenido (desasignado)" libera los recursos del equipo, como la CPU, la memoria y la red.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-181">A "Stopped (deallocated)" status releases the computer resources, such as the CPU, memory, and network.</span></span> <span data-ttu-id="3b2ac-182">Sin embargo, los discos se siguen conservando para que el usuario pueda volver a crear rápidamente la máquina virtual si fuera necesario.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-182">The disks, however, are still retained so that you can quickly re-create the VM if necessary.</span></span> <span data-ttu-id="3b2ac-183">Estos discos se crean encima de los discos duros virtuales que están respaldados por Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-183">These disks are created on top of VHDs, which are backed by Azure storage.</span></span> <span data-ttu-id="3b2ac-184">La cuenta de almacenamiento tiene estos discos duros virtuales y los discos tienen concesiones sobre esos discos duros virtuales.</span><span class="sxs-lookup"><span data-stu-id="3b2ac-184">The storage account has these VHDs, and the disks have leases on those VHDs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b2ac-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3b2ac-185">Next steps</span></span>
* [<span data-ttu-id="3b2ac-186">Eliminar una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="3b2ac-186">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
