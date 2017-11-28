---
title: aaaAttach un tooa de disco de datos administrados VM de Windows - Azure | Documentos de Microsoft
description: "El modo tooattach nueva administra datos disco tooa VM de Windows en hello Azure portal mediante Hola modelo de implementación del Administrador de recursos."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="ef354-103">¿Cómo tooattach un datos administrados disco tooa VM de Windows en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ef354-103">How tooattach a managed data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="ef354-104">Este artículo muestra cómo tooattach una nueva datos administrada disco máquinas virtuales de tooWindows a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ef354-104">This article shows you how tooattach a new managed data disk tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="ef354-105">Antes de hacerlo, revise estas sugerencias:</span><span class="sxs-lookup"><span data-stu-id="ef354-105">Before you do this, review these tips:</span></span>

* <span data-ttu-id="ef354-106">tamaño de Hola de máquina virtual de hello controla cuántos discos de datos que puede conectar.</span><span class="sxs-lookup"><span data-stu-id="ef354-106">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="ef354-107">Para obtener más información, consulte [Tamaños de máquinas virtuales](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="ef354-107">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="ef354-108">Para un disco nuevo, no es necesario toocreate lo primer porque Azure lo crea al adjuntarla.</span><span class="sxs-lookup"><span data-stu-id="ef354-108">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="ef354-109">También puede [conectar un disco de datos mediante Powershell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ef354-109">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="add-a-data-disk"></a><span data-ttu-id="ef354-110">Agregar un disco de datos</span><span class="sxs-lookup"><span data-stu-id="ef354-110">Add a data disk</span></span>
1. <span data-ttu-id="ef354-111">En el menú de Hola Hola izquierda, haga clic en **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="ef354-111">In hello menu on hello left, click **Virtual Machines**.</span></span>
2. <span data-ttu-id="ef354-112">Seleccione la máquina virtual de Hola de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef354-112">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="ef354-113">En la hoja de la máquina virtual de hello, haga clic en **discos**.</span><span class="sxs-lookup"><span data-stu-id="ef354-113">On hello virtual machine blade, click **Disks**.</span></span>
   4. <span data-ttu-id="ef354-114">En hello **discos** hoja, haga clic en **+ Agregar disco de datos**.</span><span class="sxs-lookup"><span data-stu-id="ef354-114">On hello **Disks** blade, click **+ Add data disk**.</span></span>
5. <span data-ttu-id="ef354-115">En la lista desplegable para nuevo disco de Hola Hola, seleccione **crear vacío**.</span><span class="sxs-lookup"><span data-stu-id="ef354-115">In hello drop-down for hello new disk, select **Create empty**.</span></span>
6. <span data-ttu-id="ef354-116">Hola **disco administrado crear** hoja, escriba un nombre para el disco de Hola y ajuste Hola otras opciones según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ef354-116">In hello **Create managed disk** blade, type in a name for hello disk and adjust hello other settings as necessary.</span></span> <span data-ttu-id="ef354-117">Cuando haya terminado, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ef354-117">When you are done, click **Create**.</span></span>
7. <span data-ttu-id="ef354-118">Hola **discos** hoja, haga clic en Guardar toosave Hola nueva configuración de disco para hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ef354-118">In hello **Disks** blade, click save toosave hello new disk configuration for hello VM.</span></span>
6. <span data-ttu-id="ef354-119">Después de Azure crea el disco de Hola y lo adjunta toohello virtual machine, nuevo disco de hello aparece en la configuración de disco de la máquina virtual hello en **discos de datos**.</span><span class="sxs-lookup"><span data-stu-id="ef354-119">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="initialize-a-new-data-disk"></a><span data-ttu-id="ef354-120">Inicio de un nuevo disco de datos</span><span class="sxs-lookup"><span data-stu-id="ef354-120">Initialize a new data disk</span></span>

1. <span data-ttu-id="ef354-121">Conectar toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ef354-121">Connect toohello VM.</span></span>
1. <span data-ttu-id="ef354-122">Haga clic en el menú de inicio de hello dentro de hello VM y tipo **diskmgmt.msc** y posicionamiento **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="ef354-122">Click hello start menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="ef354-123">Esto iniciará el complemento Administración de discos Hola.</span><span class="sxs-lookup"><span data-stu-id="ef354-123">This will start hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="ef354-124">Administración de discos reconocerá que tenga un disco nuevo, no inicializado y se abrirá la ventana de hello inicializar disco.</span><span class="sxs-lookup"><span data-stu-id="ef354-124">Disk Management will recognize that you have a new, un-initialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="ef354-125">Asegúrese de que se ha seleccionado Hola nuevo disco y haga clic en **Aceptar** tooinitialize lo.</span><span class="sxs-lookup"><span data-stu-id="ef354-125">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="ef354-126">nuevo disco de Hello aparecerá ahora como **sin asignar**.</span><span class="sxs-lookup"><span data-stu-id="ef354-126">hello new disk will now appear as **unallocated**.</span></span> <span data-ttu-id="ef354-127">Haga doble clic en cualquier lugar en el disco de Hola y seleccione **nuevo volumen simple**.</span><span class="sxs-lookup"><span data-stu-id="ef354-127">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="ef354-128">Hola **Asistente nuevo volumen Simple** se iniciará.</span><span class="sxs-lookup"><span data-stu-id="ef354-128">hello **New Simple Volume Wizard** will start.</span></span>
5. <span data-ttu-id="ef354-129">Vaya a través del Asistente de hello, mantener todos los valores predeterminados de hello, cuando haya terminado de seleccionar **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="ef354-129">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="ef354-130">Cierre Administración de discos.</span><span class="sxs-lookup"><span data-stu-id="ef354-130">Close Disk Management.</span></span>
7. <span data-ttu-id="ef354-131">Aparecerá una ventana emergente que necesita nuevo disco de tooformat Hola antes de utilizarla.</span><span class="sxs-lookup"><span data-stu-id="ef354-131">You will get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="ef354-132">Haga clic en **Dar formato al disco**.</span><span class="sxs-lookup"><span data-stu-id="ef354-132">Click **Format disk**.</span></span>
8. <span data-ttu-id="ef354-133">Hola **dar formato al nuevo disco** cuadro de diálogo, configuración de comprobación de hello y, a continuación, haga clic en **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="ef354-133">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="ef354-134">Recibirá una advertencia que dar formato a discos de Hola se eliminarán todos los datos de hello, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ef354-134">You will get a warning that formatting hello disks will erase all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="ef354-135">Una vez completado el formato de hello, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ef354-135">When hello format is complete, click **OK**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="ef354-136">Uso de TRIM con el almacenamiento estándar</span><span class="sxs-lookup"><span data-stu-id="ef354-136">Use TRIM with standard storage</span></span>

<span data-ttu-id="ef354-137">Si utiliza almacenamiento estándar (HDD), debe habilitar TRIM.</span><span class="sxs-lookup"><span data-stu-id="ef354-137">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="ef354-138">TRIM descarta los bloques sin utilizar en el disco de Hola, por lo que solo se le facturará de almacenamiento que utiliza realmente.</span><span class="sxs-lookup"><span data-stu-id="ef354-138">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="ef354-139">Esto puede suponerle un ahorro si crea archivos grandes y, luego, los elimina.</span><span class="sxs-lookup"><span data-stu-id="ef354-139">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="ef354-140">Puede ejecutar esta opción de RECORTE de comando toocheck Hola.</span><span class="sxs-lookup"><span data-stu-id="ef354-140">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="ef354-141">Abra un símbolo del sistema en su máquina virtual de Windows y escriba:</span><span class="sxs-lookup"><span data-stu-id="ef354-141">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="ef354-142">Si el comando de hello devuelve 0, RECORTE está habilitada correctamente.</span><span class="sxs-lookup"><span data-stu-id="ef354-142">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="ef354-143">Si devuelve 1, ejecute hello después tooenable comando RECORTE:</span><span class="sxs-lookup"><span data-stu-id="ef354-143">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="ef354-144">Después de eliminar los datos desde el disco, puede asegurarse de operaciones de RECORTE de hello vaciadas correctamente mediante la ejecución de desfragmentación con RECORTE:</span><span class="sxs-lookup"><span data-stu-id="ef354-144">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="ef354-145">También puede asegurarse de todo el volumen de Hola se recorta por formatear volumen Hola.</span><span class="sxs-lookup"><span data-stu-id="ef354-145">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef354-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ef354-146">Next steps</span></span>
<span data-ttu-id="ef354-147">Si la aplicación necesita que los datos de toouse Hola D: unidad toostore, puede [cambiar Hola la letra de unidad de disco temporal de Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ef354-147">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
