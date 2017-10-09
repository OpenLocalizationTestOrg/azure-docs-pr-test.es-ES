---
title: aaaAttach un tooa de disco de datos no administrados VM de Windows - Azure | Documentos de Microsoft
description: "¿Cómo tooattach nuevo o existente de los datos no administrados disco tooa VM de Windows en hello Azure portal mediante Hola modelo de implementación del Administrador de recursos."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="25b15-103">¿Cómo tooattach un datos no administrados disco tooa VM de Windows en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="25b15-103">How tooattach an unmanaged data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="25b15-104">Este artículo muestra cómo tooattach nueva y existente sin administrar discos máquinas virtuales de tooWindows a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="25b15-104">This article shows you how tooattach both new and existing unmanaged disks tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="25b15-105">También puede [conectar un disco de datos mediante PowerShell](./attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="25b15-105">You can also [attach a data disk using PowerShell](./attach-disk-ps.md).</span></span> <span data-ttu-id="25b15-106">Antes de hacerlo, revise estas sugerencias:</span><span class="sxs-lookup"><span data-stu-id="25b15-106">Before you do this, review these tips:</span></span>

* <span data-ttu-id="25b15-107">tamaño de Hola de máquina virtual de hello controla cuántos discos de datos que puede conectar.</span><span class="sxs-lookup"><span data-stu-id="25b15-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="25b15-108">Para obtener más información, consulte [Tamaños de máquinas virtuales](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="25b15-108">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="25b15-109">toouse almacenamiento Premium, necesita una máquina virtual DS-series o GS-series.</span><span class="sxs-lookup"><span data-stu-id="25b15-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="25b15-110">Puede utilizar discos de cuentas de almacenamiento premium y estándar con estas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="25b15-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="25b15-111">Almacenamiento premium está disponible en determinadas regiones.</span><span class="sxs-lookup"><span data-stu-id="25b15-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="25b15-112">Para obtener más información, consulte [Almacenamiento Premium: Almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="25b15-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="25b15-113">Para un disco nuevo, no es necesario toocreate lo primer porque Azure lo crea al adjuntarla.</span><span class="sxs-lookup"><span data-stu-id="25b15-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>


<span data-ttu-id="25b15-114">También puede [conectar un disco de datos mediante Powershell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="25b15-114">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="25b15-115">Encontró la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="25b15-115">Find hello virtual machine</span></span>
1. <span data-ttu-id="25b15-116">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="25b15-116">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="25b15-117">En el menú de Hola Hola izquierda, haga clic en **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="25b15-117">In hello menu on hello left, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="25b15-118">Seleccione la máquina virtual de Hola de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="25b15-118">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="25b15-119">En la hoja de máquinas virtuales de hello, haga clic en **discos**.</span><span class="sxs-lookup"><span data-stu-id="25b15-119">In hello Virtual machines blade, click **Disks**.</span></span>
   
<span data-ttu-id="25b15-120">Continúe siguiendo las instrucciones para conectar un [nuevo disco](#option-1-attach-a-new-disk) o un [disco existente](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="25b15-120">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="25b15-121">Opción 1: adjunte e inicialice un disco nuevo</span><span class="sxs-lookup"><span data-stu-id="25b15-121">Option 1: Attach and initialize a new disk</span></span>
1. <span data-ttu-id="25b15-122">En hello **discos** hoja, haga clic en **+ Agregar disco de datos**.</span><span class="sxs-lookup"><span data-stu-id="25b15-122">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="25b15-123">Hola **conectar disco administrado** hoja, escriba un nombre para el disco de hello en **nombre** y, a continuación, seleccione **New (disco vacío)** en **como tipo de origen**.</span><span class="sxs-lookup"><span data-stu-id="25b15-123">In hello **Attach managed disk** blade, type a name for hello disk in **Name** and then select **New (empty disk)** in **Source type**.</span></span>
3. <span data-ttu-id="25b15-124">En **contenedor de almacenamiento**, haga clic en hello **examinar** botón y busque la cuenta de almacenamiento de toohello y contenedor donde como Hola nuevo disco duro virtual toobe almacenado y, a continuación, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="25b15-124">Under **Storage container**, click hello **Browse** button and browse toohello storage account and container where you would like hello new VHD toobe stored and then click **Select**.</span></span> 
  
   ![Revisar configuración de disco](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. <span data-ttu-id="25b15-126">Cuando haya terminado con la configuración de Hola Hola disco de datos, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="25b15-126">When you are done with hello settings for hello data disk, click **OK**.</span></span>
4. <span data-ttu-id="25b15-127">Nuevo en hello **discos** hoja, haga clic en **guardar** configuración de máquina virtual de tooadd Hola disco toohello.</span><span class="sxs-lookup"><span data-stu-id="25b15-127">Back in hello **Disks** blade, click **Save** tooadd hello disk toohello VM configuration.</span></span>


### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="25b15-128">Inicio de un nuevo disco de datos</span><span class="sxs-lookup"><span data-stu-id="25b15-128">Initialize a new data disk</span></span>

1. <span data-ttu-id="25b15-129">Conectar la máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="25b15-129">Connect toohello virtual machine.</span></span> <span data-ttu-id="25b15-130">Para obtener instrucciones, consulte [cómo tooconnect y tooan virtual de Azure de inicio de sesión automático con Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="25b15-130">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
1. <span data-ttu-id="25b15-131">Haga clic en hello **iniciar** menú dentro de hello VM y escriba **diskmgmt.msc** y posicionamiento **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="25b15-131">Click hello **Start** menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="25b15-132">Esto inicia el complemento Administración de discos Hola.</span><span class="sxs-lookup"><span data-stu-id="25b15-132">This starts hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="25b15-133">Administración de discos reconoce que tiene un disco nuevo sin inicializar y se abrirá la ventana de hello inicializar disco.</span><span class="sxs-lookup"><span data-stu-id="25b15-133">Disk Management recognizes that you have a new, uninitialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="25b15-134">Asegúrese de que se ha seleccionado Hola nuevo disco y haga clic en **Aceptar** tooinitialize lo.</span><span class="sxs-lookup"><span data-stu-id="25b15-134">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="25b15-135">Hello nuevo disco aparece ahora como **sin asignar**.</span><span class="sxs-lookup"><span data-stu-id="25b15-135">hello new disk now appears as **unallocated**.</span></span> <span data-ttu-id="25b15-136">Haga doble clic en cualquier lugar en el disco de Hola y seleccione **nuevo volumen simple**.</span><span class="sxs-lookup"><span data-stu-id="25b15-136">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="25b15-137">Hola **Asistente nuevo volumen Simple** inicia.</span><span class="sxs-lookup"><span data-stu-id="25b15-137">hello **New Simple Volume Wizard** starts.</span></span>
5. <span data-ttu-id="25b15-138">Vaya a través del Asistente de hello, mantener todos los valores predeterminados de hello, cuando haya terminado de seleccionar **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="25b15-138">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="25b15-139">Cierre Administración de discos.</span><span class="sxs-lookup"><span data-stu-id="25b15-139">Close Disk Management.</span></span>
7. <span data-ttu-id="25b15-140">Obtiene un elemento emergente que necesita nuevo disco de tooformat Hola antes de utilizarla.</span><span class="sxs-lookup"><span data-stu-id="25b15-140">You get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="25b15-141">Haga clic en **Dar formato al disco**.</span><span class="sxs-lookup"><span data-stu-id="25b15-141">Click **Format disk**.</span></span>
8. <span data-ttu-id="25b15-142">Hola **dar formato al nuevo disco** cuadro de diálogo, configuración de comprobación de hello y, a continuación, haga clic en **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="25b15-142">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="25b15-143">Recibe una advertencia que dar formato a discos de hello borra todos los datos de hello, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="25b15-143">You get a warning that formatting hello disks erases all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="25b15-144">Una vez completado el formato de hello, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="25b15-144">When hello format is complete, click **OK**.</span></span>


## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="25b15-145">Opción 2: Conectar un disco existente</span><span class="sxs-lookup"><span data-stu-id="25b15-145">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="25b15-146">En hello **discos** hoja, haga clic en **+ Agregar disco de datos**.</span><span class="sxs-lookup"><span data-stu-id="25b15-146">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="25b15-147">En hello **conectar disco no administrado** hoja, en **tipo de origen de** seleccione **blob existente**.</span><span class="sxs-lookup"><span data-stu-id="25b15-147">On hello **Attach unmanaged disk** blade, in **Source type** select **Existing blob**.</span></span>

    ![Revisar configuración de disco](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. <span data-ttu-id="25b15-149">Haga clic en **examinar** toonavigate toohello cuenta de almacenamiento y contenedor donde hello disco duro virtual existente se encuentra.</span><span class="sxs-lookup"><span data-stu-id="25b15-149">Click **Browse** toonavigate toohello storage account and container where hello existing VHD is located.</span></span> <span data-ttu-id="25b15-150">Haga clic en y Hola VHD y, a continuación, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="25b15-150">Click and hello VHD and then click **Select**.</span></span>
4. <span data-ttu-id="25b15-151">Haga clic en **Aceptar** en hello **conectar disco no administrado** hoja.</span><span class="sxs-lookup"><span data-stu-id="25b15-151">Click **OK** in hello **Attach unmanaged disk** blade.</span></span>
5. <span data-ttu-id="25b15-152">Hola **discos** hoja, haga clic en **guardar** tooadd hello toohello configuración de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="25b15-152">In hello **Disks** blade, click **Save** tooadd hello disk toohello configuration for hello VM.</span></span>
   


## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="25b15-153">Uso de TRIM con el almacenamiento estándar</span><span class="sxs-lookup"><span data-stu-id="25b15-153">Use TRIM with standard storage</span></span>

<span data-ttu-id="25b15-154">Si utiliza almacenamiento estándar (HDD), debe habilitar TRIM.</span><span class="sxs-lookup"><span data-stu-id="25b15-154">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="25b15-155">TRIM descarta los bloques sin utilizar en el disco de Hola, por lo que solo se le facturará de almacenamiento que utiliza realmente.</span><span class="sxs-lookup"><span data-stu-id="25b15-155">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="25b15-156">Esto puede suponerle un ahorro si crea archivos grandes y, luego, los elimina.</span><span class="sxs-lookup"><span data-stu-id="25b15-156">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="25b15-157">Puede ejecutar esta opción de RECORTE de comando toocheck Hola.</span><span class="sxs-lookup"><span data-stu-id="25b15-157">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="25b15-158">Abra un símbolo del sistema en su máquina virtual de Windows y escriba:</span><span class="sxs-lookup"><span data-stu-id="25b15-158">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="25b15-159">Si el comando de hello devuelve 0, RECORTE está habilitada correctamente.</span><span class="sxs-lookup"><span data-stu-id="25b15-159">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="25b15-160">Si devuelve 1, ejecute hello después tooenable comando RECORTE:</span><span class="sxs-lookup"><span data-stu-id="25b15-160">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="25b15-161">Después de eliminar los datos desde el disco, puede asegurarse de operaciones de RECORTE de hello vaciadas correctamente mediante la ejecución de desfragmentación con RECORTE:</span><span class="sxs-lookup"><span data-stu-id="25b15-161">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="25b15-162">También puede asegurarse de todo el volumen de Hola se recorta por formatear volumen Hola.</span><span class="sxs-lookup"><span data-stu-id="25b15-162">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>


## <a name="next-steps"></a><span data-ttu-id="25b15-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="25b15-163">Next steps</span></span>
<span data-ttu-id="25b15-164">Si la aplicación necesita que los datos de toouse Hola D: unidad toostore, puede [cambiar Hola la letra de unidad de disco temporal de Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="25b15-164">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

