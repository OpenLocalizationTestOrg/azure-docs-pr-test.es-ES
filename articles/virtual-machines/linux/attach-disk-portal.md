---
title: aaaAttach un tooa de disco de datos VM de Linux | Documentos de Microsoft
description: "¿Cómo tooattach datos nuevos o existentes disco tooa VM de Linux en hello Azure portal mediante Hola modelo de implementación del Administrador de recursos."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a><span data-ttu-id="9bee7-103">¿Cómo tooattach datos de un disco tooa VM de Linux en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9bee7-103">How tooattach a data disk tooa Linux VM in hello Azure portal</span></span>
<span data-ttu-id="9bee7-104">Este artículo muestra cómo tooattach nueva y existente discos de máquina virtual de Linux tooa a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9bee7-104">This article shows you how tooattach both new and existing disks tooa Linux virtual machine through hello Azure portal.</span></span> <span data-ttu-id="9bee7-105">También puede [adjuntar un tooa de disco de datos VM de Windows en el portal de Azure hello](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9bee7-105">You can also [attach a data disk tooa Windows VM in hello Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="9bee7-106">Puede elegir toouse en discos de Azure administrados o no administrada de discos.</span><span class="sxs-lookup"><span data-stu-id="9bee7-106">You can choose toouse either Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="9bee7-107">Discos administrados se controlan mediante la plataforma Windows Azure hello y no requieren ningún toostore los preparativos o ubicación ellos.</span><span class="sxs-lookup"><span data-stu-id="9bee7-107">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="9bee7-108">Los discos no administrados requieren una cuenta de almacenamiento y tienen algunas [cuotas y límites que se deben aplicar](../../azure-subscription-service-limits.md#storage-limits).</span><span class="sxs-lookup"><span data-stu-id="9bee7-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="9bee7-109">Para más información sobre Azure Managed Disks, consulte [Azure Managed Disks overview](../windows/managed-disks-overview.md) (Introducción a Azure Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="9bee7-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="9bee7-110">Antes de adjuntar discos tooyour VM, revise estas sugerencias:</span><span class="sxs-lookup"><span data-stu-id="9bee7-110">Before you attach disks tooyour VM, review these tips:</span></span>

* <span data-ttu-id="9bee7-111">tamaño de Hola de máquina virtual de hello controla cuántos discos de datos que puede conectar.</span><span class="sxs-lookup"><span data-stu-id="9bee7-111">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="9bee7-112">Para obtener más información, consulte [Tamaños de máquinas virtuales](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9bee7-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="9bee7-113">toouse almacenamiento Premium, necesita una máquina virtual DS-series o GS-series.</span><span class="sxs-lookup"><span data-stu-id="9bee7-113">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="9bee7-114">Puede usar discos Premium y Estándar con estas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9bee7-114">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="9bee7-115">Almacenamiento premium está disponible en determinadas regiones.</span><span class="sxs-lookup"><span data-stu-id="9bee7-115">Premium storage is available in certain regions.</span></span> <span data-ttu-id="9bee7-116">Para obtener más información, consulte [Almacenamiento Premium: Almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="9bee7-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="9bee7-117">Discos conectados toovirtual máquinas son realmente los archivos .vhd almacenados en Azure.</span><span class="sxs-lookup"><span data-stu-id="9bee7-117">Disks attached toovirtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="9bee7-118">Para obtener más información, vea [Acerca de los discos y los discos duros virtuales para máquinas virtuales](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9bee7-118">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="9bee7-119">Encontró la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="9bee7-119">Find hello virtual machine</span></span>
1. <span data-ttu-id="9bee7-120">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9bee7-120">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9bee7-121">En el menú del concentrador hello, haga clic en **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="9bee7-121">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="9bee7-122">Seleccione la máquina virtual de Hola de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee7-122">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="9bee7-123">toohello Virtual hoja, los equipos en **Essentials**, haga clic en **discos**.</span><span class="sxs-lookup"><span data-stu-id="9bee7-123">toohello Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![Abrir configuración de disco](./media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="9bee7-125">Para continuar, siga las instrucciones y conecte un [disco administrado](#use-azure-managed-disks) o un [disco no administrado](#use-unmanaged-disks).</span><span class="sxs-lookup"><span data-stu-id="9bee7-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span></span>

## <a name="use-azure-managed-disks"></a><span data-ttu-id="9bee7-126">Uso de Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="9bee7-126">Use Azure Managed Disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="9bee7-127">Conexión de un disco nuevo</span><span class="sxs-lookup"><span data-stu-id="9bee7-127">Attach a new disk</span></span>

1. <span data-ttu-id="9bee7-128">En hello **discos** hoja, haga clic en **+ Agregar disco de datos**.</span><span class="sxs-lookup"><span data-stu-id="9bee7-128">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="9bee7-129">Haga clic en el menú desplegable de Hola para **nombre** y seleccione **crear disco**:</span><span class="sxs-lookup"><span data-stu-id="9bee7-129">Click hello drop-down menu for **Name** and select **Create disk**:</span></span>

    ![Creación de disco administrado de Azure](./media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="9bee7-131">Escriba un nombre para el disco administrado.</span><span class="sxs-lookup"><span data-stu-id="9bee7-131">Enter a name for your managed disk.</span></span> <span data-ttu-id="9bee7-132">Revise la configuración predeterminada de hello, actualizar según sea necesario y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="9bee7-132">Review hello default settings, update as necessary, and then click **Create**.</span></span>
   
   ![Revisar configuración de disco](./media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="9bee7-134">Haga clic en **guardar** toocreate Hola administrados disco y actualización de configuración de máquina virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="9bee7-134">Click **Save** toocreate hello managed disk and update hello VM configuration:</span></span>

   ![Guardado del nuevo Azure Managed Disk](./media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="9bee7-136">Después de Azure crea el disco de Hola y lo adjunta toohello virtual machine, nuevo disco de hello aparece en la configuración de disco de la máquina virtual hello en **discos de datos**.</span><span class="sxs-lookup"><span data-stu-id="9bee7-136">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="9bee7-137">Como discos administrados son un recurso de nivel superior, disco de hello aparece en la raíz de Hola Hola del grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="9bee7-137">As managed disks are a top-level resource, hello disk appears at hello root of hello resource group:</span></span>

   ![Azure Managed Disk en grupo de recursos](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a><span data-ttu-id="9bee7-139">un disco existente</span><span class="sxs-lookup"><span data-stu-id="9bee7-139">Attach an existing disk</span></span>
1. <span data-ttu-id="9bee7-140">En hello **discos** hoja, haga clic en **+ Agregar disco de datos**.</span><span class="sxs-lookup"><span data-stu-id="9bee7-140">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="9bee7-141">Haga clic en el menú desplegable de Hola para **nombre** tooview una lista de las administra discos accesible tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9bee7-141">Click hello drop-down menu for **Name** tooview a list of existing managed disks accessible tooyour Azure subscription.</span></span> <span data-ttu-id="9bee7-142">Seleccione Hola administrado tooattach de disco:</span><span class="sxs-lookup"><span data-stu-id="9bee7-142">Select hello managed disk tooattach:</span></span>

   ![Conexión de un disco administrado de Azure existente](./media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="9bee7-144">Haga clic en **guardar** tooattach Hola existente administrado disco y actualización de configuración de máquina virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="9bee7-144">Click **Save** tooattach hello existing managed disk and update hello VM configuration:</span></span>
   
   ![Guardado de las actualizaciones del disco administrado de Azure](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="9bee7-146">Después de que Azure asocia hello disco toohello virtual machine, aparece en la configuración de disco de la máquina virtual hello en **discos de datos**.</span><span class="sxs-lookup"><span data-stu-id="9bee7-146">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-unmanaged-disks"></a><span data-ttu-id="9bee7-147">Uso de discos no administrados</span><span class="sxs-lookup"><span data-stu-id="9bee7-147">Use unmanaged disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="9bee7-148">Conexión de un disco nuevo</span><span class="sxs-lookup"><span data-stu-id="9bee7-148">Attach a new disk</span></span>

1. <span data-ttu-id="9bee7-149">En hello **discos** hoja, haga clic en **+ Agregar disco de datos**.</span><span class="sxs-lookup"><span data-stu-id="9bee7-149">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="9bee7-150">Revise la configuración predeterminada de hello, actualizar según sea necesario y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9bee7-150">Review hello default settings, update as necessary, and then click **OK**.</span></span>
   
   ![Revisar configuración de disco](./media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="9bee7-152">Después de Azure crea el disco de Hola y lo adjunta toohello virtual machine, nuevo disco de hello aparece en la configuración de disco de la máquina virtual hello en **discos de datos**.</span><span class="sxs-lookup"><span data-stu-id="9bee7-152">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="9bee7-153">un disco existente</span><span class="sxs-lookup"><span data-stu-id="9bee7-153">Attach an existing disk</span></span>
1. <span data-ttu-id="9bee7-154">En hello **discos** hoja, haga clic en **+ Agregar disco de datos**.</span><span class="sxs-lookup"><span data-stu-id="9bee7-154">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="9bee7-155">En **Adjuntar un disco existente**, haga clic en **Archivo VHD**.</span><span class="sxs-lookup"><span data-stu-id="9bee7-155">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![Conectar disco existente](./media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="9bee7-157">En **cuentas de almacenamiento**, seleccione la cuenta de hello y contenedor que contiene el archivo .vhd de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee7-157">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>
   
   ![Buscar ubicación de VHD](./media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="9bee7-159">Seleccione el archivo .vhd de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee7-159">Select hello .vhd file.</span></span>
5. <span data-ttu-id="9bee7-160">En **adjuntar el disco existente**, aparece el archivo hello que acaba de seleccionar en **archivo VHD**.</span><span class="sxs-lookup"><span data-stu-id="9bee7-160">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="9bee7-161">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9bee7-161">Click **OK**.</span></span>
6. <span data-ttu-id="9bee7-162">Después de que Azure asocia hello disco toohello virtual machine, aparece en la configuración de disco de la máquina virtual hello en **discos de datos**.</span><span class="sxs-lookup"><span data-stu-id="9bee7-162">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9bee7-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9bee7-163">Next steps</span></span>
<span data-ttu-id="9bee7-164">Después de agrega el disco de hello, necesita tooprepare, para su uso.</span><span class="sxs-lookup"><span data-stu-id="9bee7-164">After hello disk is added, you need tooprepare it for use.</span></span> <span data-ttu-id="9bee7-165">Para obtener más información, consulte [Inicio de un nuevo disco de datos](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="9bee7-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span></span>
