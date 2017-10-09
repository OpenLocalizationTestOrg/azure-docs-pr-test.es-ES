---
title: "aaaAttach un tooa de disco virtual de Azure clásico | Documentos de Microsoft"
description: "Conectar una máquina de virtual datos disco tooa Windows creada con el modelo de implementación clásica de hello e inicializarlo."
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="48825-103">Conectar una máquina de virtual datos disco tooa Windows creada con el modelo de implementación clásica de Hola</span><span class="sxs-lookup"><span data-stu-id="48825-103">Attach a data disk tooa Windows virtual machine created with hello classic deployment model</span></span>
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="48825-104">Este artículo muestra cómo los discos nuevos y existentes tooattach crean con hello clásico implementación modelo tooa máquina virtual de Windows con hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="48825-104">This article shows you how tooattach new and existing disks created with hello Classic deployment model tooa Windows virtual machine using hello Azure portal.</span></span>

<span data-ttu-id="48825-105">También puede [adjuntar un tooa de disco de datos VM de Linux en el portal de Azure hello](../../linux/attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="48825-105">You can also [attach a data disk tooa Linux VM in hello Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="48825-106">Antes de conectar un disco, revise estas sugerencias:</span><span class="sxs-lookup"><span data-stu-id="48825-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="48825-107">tamaño de Hola de máquina virtual de hello controla cuántos discos de datos que puede conectar.</span><span class="sxs-lookup"><span data-stu-id="48825-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="48825-108">Para obtener más información, consulte [Tamaños de máquinas virtuales](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="48825-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="48825-109">toouse almacenamiento Premium, necesita una máquina virtual DS-series o GS-series.</span><span class="sxs-lookup"><span data-stu-id="48825-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="48825-110">Puede utilizar discos de cuentas de almacenamiento premium y estándar con estas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="48825-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="48825-111">Almacenamiento premium está disponible en determinadas regiones.</span><span class="sxs-lookup"><span data-stu-id="48825-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="48825-112">Para obtener más información, consulte [Almacenamiento Premium: Almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="48825-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="48825-113">Para un disco nuevo, no es necesario toocreate lo primer porque Azure lo crea al adjuntarla.</span><span class="sxs-lookup"><span data-stu-id="48825-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="48825-114">También puede [conectar un disco de datos mediante Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="48825-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48825-115">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="48825-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-hello-virtual-machine"></a><span data-ttu-id="48825-116">Encontró la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="48825-116">Find hello virtual machine</span></span>
1. <span data-ttu-id="48825-117">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="48825-117">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="48825-118">Hola seleccione la máquina virtual del recurso de hello aparece en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="48825-118">Select hello virtual machine from hello resource listed on hello dashboard.</span></span>
3. <span data-ttu-id="48825-119">En el panel izquierdo de hello en **configuración**, haga clic en **discos**.</span><span class="sxs-lookup"><span data-stu-id="48825-119">In hello left pane under **Settings**, click **Disks**.</span></span>

    ![Abrir configuración de disco](./media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="48825-121">Continúe siguiendo las instrucciones para conectar un [nuevo disco](#option-1-attach-a-new-disk) o un [disco existente](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="48825-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="48825-122">Opción 1: adjunte e inicialice un disco nuevo</span><span class="sxs-lookup"><span data-stu-id="48825-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="48825-123">En hello **discos** hoja, haga clic en **adjuntar nuevas**.</span><span class="sxs-lookup"><span data-stu-id="48825-123">On hello **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="48825-124">Revise la configuración predeterminada de hello, actualizar según sea necesario y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="48825-124">Review hello default settings, update as necessary, and then click **OK**.</span></span>

   ![Revisar configuración de disco](./media/attach-disk/attach-new.png)

3. <span data-ttu-id="48825-126">Después de Azure crea el disco de Hola y lo adjunta toohello virtual machine, nuevo disco de hello aparece en la configuración de disco de la máquina virtual hello en **discos de datos**.</span><span class="sxs-lookup"><span data-stu-id="48825-126">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="48825-127">Inicio de un nuevo disco de datos</span><span class="sxs-lookup"><span data-stu-id="48825-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="48825-128">Conectar la máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="48825-128">Connect toohello virtual machine.</span></span> <span data-ttu-id="48825-129">Para obtener instrucciones, consulte [cómo tooconnect y tooan virtual de Azure de inicio de sesión automático con Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="48825-129">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="48825-130">Una vez que ha iniciado sesión en la máquina virtual de toohello, abra **el administrador del servidor**.</span><span class="sxs-lookup"><span data-stu-id="48825-130">After you log on toohello virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="48825-131">En el panel izquierdo de hello, seleccione **File and Storage Services**.</span><span class="sxs-lookup"><span data-stu-id="48825-131">In hello left pane, select **File and Storage Services**.</span></span>

    ![Abrir Administrador de servidores](../media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="48825-133">Seleccione **Discos**.</span><span class="sxs-lookup"><span data-stu-id="48825-133">Select **Disks**.</span></span>
4. <span data-ttu-id="48825-134">Hola **discos** sección enumera los discos de Hola.</span><span class="sxs-lookup"><span data-stu-id="48825-134">hello **Disks** section lists hello disks.</span></span> <span data-ttu-id="48825-135">A menudo, una máquina virtual tiene los discos 0, 1 y 2.</span><span class="sxs-lookup"><span data-stu-id="48825-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="48825-136">El disco 0 es el disco del sistema operativo de hello, disco 1 es el disco temporal de Hola y el disco 2 es el disco de datos de hello recién conectado toohello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="48825-136">Disk 0 is hello operating system disk, disk 1 is hello temporary disk, and disk 2 is hello data disk newly attached toohello virtual machine.</span></span> <span data-ttu-id="48825-137">listas de disco de datos Hola Hola partición como **desconocido**.</span><span class="sxs-lookup"><span data-stu-id="48825-137">hello data disk lists hello Partition as **Unknown**.</span></span>

 <span data-ttu-id="48825-138">Haga clic en el disco de Hola y seleccione **inicializar**.</span><span class="sxs-lookup"><span data-stu-id="48825-138">Right-click hello disk and select **Initialize**.</span></span>

5. <span data-ttu-id="48825-139">Se le notificará que se borrarán todos los datos cuando se inicializa el disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="48825-139">You're notified that all data will be erased when hello disk is initialized.</span></span> <span data-ttu-id="48825-140">Haga clic en **Sí** tooacknowledge disco de hello advertencia e inicialice Hola.</span><span class="sxs-lookup"><span data-stu-id="48825-140">Click **Yes** tooacknowledge hello warning and initialize hello disk.</span></span> <span data-ttu-id="48825-141">Una vez completado, se enumerarán como partición de hello **GPT**.</span><span class="sxs-lookup"><span data-stu-id="48825-141">Once complete, hello partition will be listed as **GPT**.</span></span> <span data-ttu-id="48825-142">Haga clic en el disco de Hola de nuevo y seleccione **nuevo volumen**.</span><span class="sxs-lookup"><span data-stu-id="48825-142">Right-click hello disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="48825-143">Asistente de hello completa con los valores predeterminados de Hola.</span><span class="sxs-lookup"><span data-stu-id="48825-143">Complete hello wizard using hello default values.</span></span> <span data-ttu-id="48825-144">Cuando se realiza el Asistente de hello, Hola **volúmenes** sección enumeran nuevo volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="48825-144">When hello wizard is done, hello **Volumes** section lists hello new volume.</span></span> <span data-ttu-id="48825-145">Hola disco ya está en línea y lista toostore datos.</span><span class="sxs-lookup"><span data-stu-id="48825-145">hello disk is now online and ready toostore data.</span></span>

    ![Volumen inicializado correctamente](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="48825-147">Opción 2: Conectar un disco existente</span><span class="sxs-lookup"><span data-stu-id="48825-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="48825-148">En hello **discos** hoja, haga clic en **adjuntar existente**.</span><span class="sxs-lookup"><span data-stu-id="48825-148">On hello **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="48825-149">En **Adjuntar un disco existente**, haga clic en **Ubicación**.</span><span class="sxs-lookup"><span data-stu-id="48825-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![Conectar disco existente](./media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="48825-151">En **cuentas de almacenamiento**, seleccione la cuenta de hello y contenedor que contiene el archivo .vhd de Hola.</span><span class="sxs-lookup"><span data-stu-id="48825-151">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>

   ![Buscar ubicación de VHD](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="48825-153">Seleccione el archivo .vhd de Hola.</span><span class="sxs-lookup"><span data-stu-id="48825-153">Select hello .vhd file.</span></span>
5. <span data-ttu-id="48825-154">En **adjuntar el disco existente**, aparece el archivo hello que acaba de seleccionar en **archivo VHD**.</span><span class="sxs-lookup"><span data-stu-id="48825-154">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="48825-155">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="48825-155">Click **OK**.</span></span>
6. <span data-ttu-id="48825-156">Después de que Azure asocia hello disco toohello virtual machine, aparece en la configuración de disco de la máquina virtual hello en **discos de datos**.</span><span class="sxs-lookup"><span data-stu-id="48825-156">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="48825-157">Uso de TRIM con el almacenamiento estándar</span><span class="sxs-lookup"><span data-stu-id="48825-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="48825-158">Si utiliza almacenamiento estándar (HDD), debe habilitar TRIM.</span><span class="sxs-lookup"><span data-stu-id="48825-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="48825-159">TRIM descarta los bloques sin utilizar en el disco de Hola, por lo que solo se le facturará de almacenamiento que utiliza realmente.</span><span class="sxs-lookup"><span data-stu-id="48825-159">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="48825-160">Puede ahorrar costos si usa TRIM, además de los bloques sin utilizar por eliminar archivos de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="48825-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="48825-161">Puede ejecutar esta opción de RECORTE de comando toocheck Hola.</span><span class="sxs-lookup"><span data-stu-id="48825-161">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="48825-162">Abra un símbolo del sistema en su máquina virtual de Windows y escriba:</span><span class="sxs-lookup"><span data-stu-id="48825-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="48825-163">Si el comando de hello devuelve 0, RECORTE está habilitada correctamente.</span><span class="sxs-lookup"><span data-stu-id="48825-163">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="48825-164">Si devuelve 1, ejecute hello después tooenable comando RECORTE:</span><span class="sxs-lookup"><span data-stu-id="48825-164">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="48825-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="48825-165">Next steps</span></span>
<span data-ttu-id="48825-166">Si la aplicación necesita datos de toostore de la unidad D: de toouse hello, puede [cambiar Hola la letra de unidad de disco temporal de Windows hello](../../virtual-machines-windows-change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="48825-166">If your application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48825-167">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="48825-167">Additional resources</span></span>
[<span data-ttu-id="48825-168">Acerca de los discos y los discos duros virtuales para máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="48825-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)
