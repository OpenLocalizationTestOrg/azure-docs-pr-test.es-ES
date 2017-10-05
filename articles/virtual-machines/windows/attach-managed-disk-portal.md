---
title: "Conexión de un disco de datos administrado a una VM con Windows: Azure | Microsoft Docs"
description: "Se muestra cómo conectar un nuevo disco de datos administrado a una máquina virtual con Windows en Azure Portal con el modelo de implementación de Resource Manager."
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
ms.openlocfilehash: f0cf88a06c5470ef173b22e7213419a6c8760723
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-a-managed-data-disk-to-a-windows-vm-in-the-azure-portal"></a><span data-ttu-id="eb914-103">Cómo conectar un disco de datos administrado a una VM con Windows en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="eb914-103">How to attach a managed data disk to a Windows VM in the Azure portal</span></span>

<span data-ttu-id="eb914-104">En este artículo se muestra cómo conectar un nuevo disco de datos administrado a una máquina virtual con Windows a través de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="eb914-104">This article shows you how to attach a new managed data disk to Windows virtual machines through the Azure portal.</span></span> <span data-ttu-id="eb914-105">Antes de hacerlo, revise estas sugerencias:</span><span class="sxs-lookup"><span data-stu-id="eb914-105">Before you do this, review these tips:</span></span>

* <span data-ttu-id="eb914-106">El tamaño de la máquina virtual controla cuántos discos de datos puede conectar.</span><span class="sxs-lookup"><span data-stu-id="eb914-106">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="eb914-107">Para obtener más información, consulte [Tamaños de máquinas virtuales](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="eb914-107">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="eb914-108">Para un disco nuevo, no es necesario crearlo en primer lugar porque Azure lo crea cuando lo conecta.</span><span class="sxs-lookup"><span data-stu-id="eb914-108">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="eb914-109">También puede [conectar un disco de datos mediante Powershell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="eb914-109">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="add-a-data-disk"></a><span data-ttu-id="eb914-110">Agregar un disco de datos</span><span class="sxs-lookup"><span data-stu-id="eb914-110">Add a data disk</span></span>
1. <span data-ttu-id="eb914-111">En el menú izquierdo, haga clic en **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="eb914-111">In the menu on the left, click **Virtual Machines**.</span></span>
2. <span data-ttu-id="eb914-112">Seleccione la máquina virtual en la lista.</span><span class="sxs-lookup"><span data-stu-id="eb914-112">Select the virtual machine from the list.</span></span>
3. <span data-ttu-id="eb914-113">En la hoja de la máquina virtual, haga clic en **Discos**.</span><span class="sxs-lookup"><span data-stu-id="eb914-113">On the virtual machine blade, click **Disks**.</span></span>
   4. <span data-ttu-id="eb914-114">En la hoja **Discos**, haga clic en **+ Add data disk** (+ Agregar disco de datos).</span><span class="sxs-lookup"><span data-stu-id="eb914-114">On the **Disks** blade, click **+ Add data disk**.</span></span>
5. <span data-ttu-id="eb914-115">En la lista desplegable para el nuevo disco, seleccione **Crear vacío**.</span><span class="sxs-lookup"><span data-stu-id="eb914-115">In the drop-down for the new disk, select **Create empty**.</span></span>
6. <span data-ttu-id="eb914-116">En la hoja **Crear disco administrado**, escriba un nombre para el disco y ajuste las demás opciones de configuración según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="eb914-116">In the **Create managed disk** blade, type in a name for the disk and adjust the other settings as necessary.</span></span> <span data-ttu-id="eb914-117">Cuando haya terminado, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="eb914-117">When you are done, click **Create**.</span></span>
7. <span data-ttu-id="eb914-118">En la hoja **Discos**, haga clic en Guardar para guardar la configuración del nuevo disco de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eb914-118">In the **Disks** blade, click save to save the new disk configuration for the VM.</span></span>
6. <span data-ttu-id="eb914-119">Una vez que Azure crea el disco y lo adjunta a la máquina virtual, el nuevo disco aparece en la configuración de disco de la máquina virtual en el apartado **Discos de datos**.</span><span class="sxs-lookup"><span data-stu-id="eb914-119">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="initialize-a-new-data-disk"></a><span data-ttu-id="eb914-120">Inicio de un nuevo disco de datos</span><span class="sxs-lookup"><span data-stu-id="eb914-120">Initialize a new data disk</span></span>

1. <span data-ttu-id="eb914-121">Conectar a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eb914-121">Connect to the VM.</span></span>
1. <span data-ttu-id="eb914-122">Haga clic en el menú Inicio dentro de la máquina virtual, escriba **diskmgmt.msc** y presione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="eb914-122">Click the start menu inside the VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="eb914-123">Se iniciará el complemento Administración de discos.</span><span class="sxs-lookup"><span data-stu-id="eb914-123">This will start the Disk Management snap-in.</span></span>
2. <span data-ttu-id="eb914-124">Administración de discos reconocerá que hay un nuevo disco sin inicializar y se abrirá la ventana Inicializar disco.</span><span class="sxs-lookup"><span data-stu-id="eb914-124">Disk Management will recognize that you have a new, un-initialized disk and the Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="eb914-125">Asegúrese de que el nuevo disco está seleccionado y haga clic en **Aceptar** para inicializarlo.</span><span class="sxs-lookup"><span data-stu-id="eb914-125">Make sure the new disk is selected and click **OK** to initialize it.</span></span>
4. <span data-ttu-id="eb914-126">El nuevo disco aparecerá ahora como **sin asignar**.</span><span class="sxs-lookup"><span data-stu-id="eb914-126">The new disk will now appear as **unallocated**.</span></span> <span data-ttu-id="eb914-127">Haga clic con el botón derecho en cualquier lugar del disco y seleccione **Nuevo volumen simple**.</span><span class="sxs-lookup"><span data-stu-id="eb914-127">Right-click anywhere on the disk and select **New simple volume**.</span></span> <span data-ttu-id="eb914-128">Se iniciará el **Asistente para nuevo volumen simple**.</span><span class="sxs-lookup"><span data-stu-id="eb914-128">The **New Simple Volume Wizard** will start.</span></span>
5. <span data-ttu-id="eb914-129">Navegue por el asistente, conserve todos los valores predeterminados y, cuando haya terminado, seleccione **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="eb914-129">Go through the wizard, keeping all of the defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="eb914-130">Cierre Administración de discos.</span><span class="sxs-lookup"><span data-stu-id="eb914-130">Close Disk Management.</span></span>
7. <span data-ttu-id="eb914-131">Se abrirá una ventana emergente necesaria para formatear el nuevo disco para poder usarlo.</span><span class="sxs-lookup"><span data-stu-id="eb914-131">You will get a pop-up that you need to format the new disk before you can use it.</span></span> <span data-ttu-id="eb914-132">Haga clic en **Dar formato al disco**.</span><span class="sxs-lookup"><span data-stu-id="eb914-132">Click **Format disk**.</span></span>
8. <span data-ttu-id="eb914-133">En el cuadro de diálogo **Formatear disco nuevo**, active las opciones y haga clic en **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="eb914-133">In the **Format new disk** dialog, check the settings and then click **Start**.</span></span>
9. <span data-ttu-id="eb914-134">Recibirá una advertencia sobre que al formatear los discos se borrarán todos los datos, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="eb914-134">You will get a warning that formatting the disks will erase all of the data, click **OK**.</span></span>
10. <span data-ttu-id="eb914-135">Una vez completado el formato, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="eb914-135">When the format is complete, click **OK**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="eb914-136">Uso de TRIM con el almacenamiento estándar</span><span class="sxs-lookup"><span data-stu-id="eb914-136">Use TRIM with standard storage</span></span>

<span data-ttu-id="eb914-137">Si utiliza almacenamiento estándar (HDD), debe habilitar TRIM.</span><span class="sxs-lookup"><span data-stu-id="eb914-137">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="eb914-138">TRIM descarta los bloques sin utilizar del disco, por lo que solo se le facturará el almacenamiento que utiliza realmente.</span><span class="sxs-lookup"><span data-stu-id="eb914-138">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="eb914-139">Esto puede suponerle un ahorro si crea archivos grandes y, luego, los elimina.</span><span class="sxs-lookup"><span data-stu-id="eb914-139">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="eb914-140">Puede ejecutar este comando para comprobar la configuración de TRIM.</span><span class="sxs-lookup"><span data-stu-id="eb914-140">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="eb914-141">Abra un símbolo del sistema en su máquina virtual de Windows y escriba:</span><span class="sxs-lookup"><span data-stu-id="eb914-141">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="eb914-142">Si el comando devuelve 0, significa que TRIM está habilitada correctamente.</span><span class="sxs-lookup"><span data-stu-id="eb914-142">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="eb914-143">Si devuelve 1, ejecute el siguiente comando para habilitar TRIM:</span><span class="sxs-lookup"><span data-stu-id="eb914-143">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="eb914-144">Después de eliminar los datos del disco, puede garantizar que las operaciones de TRIM se vacían correctamente mediante la ejecución de desfragmentación con TRIM:</span><span class="sxs-lookup"><span data-stu-id="eb914-144">After deleting data from your disk, you can ensure the TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="eb914-145">También puede formatear el volumen para asegurarse de que quede recortado por completo.</span><span class="sxs-lookup"><span data-stu-id="eb914-145">You can also ensure the entire volume is trimmed by formatting the volume.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb914-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eb914-146">Next steps</span></span>
<span data-ttu-id="eb914-147">Si la aplicación debe usar la unidad D: para almacenar datos, puede [cambiar la letra de la unidad del disco temporal de Windows](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eb914-147">If you application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
