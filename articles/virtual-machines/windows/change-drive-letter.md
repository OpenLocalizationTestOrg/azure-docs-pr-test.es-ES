---
title: "Conversión de la unidad D: de una máquina virtual en un disco de datos | Microsoft Docs"
description: "Se describe cómo cambiar las letras de unidad de una máquina virtual de Windows para poder usar la unidad D: como unidad de datos."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 7667175c01be2421bfc3badd83b1d8aaeb29bfde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-d-drive-as-a-data-drive-on-a-windows-vm"></a><span data-ttu-id="839ca-103">Uso de la unidad de disco D: como unidad de datos en una máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="839ca-103">Use the D: drive as a data drive on a Windows VM</span></span>
<span data-ttu-id="839ca-104">Si su aplicación necesita usar la unidad D para almacenar datos, siga estas instrucciones para usar una unidad distinta para el disco temporal.</span><span class="sxs-lookup"><span data-stu-id="839ca-104">If your application needs to use the D drive to store data, follow these instructions to use a different drive letter for the temporary disk.</span></span> <span data-ttu-id="839ca-105">Nunca use el disco temporal para almacenar los datos que desee conservar.</span><span class="sxs-lookup"><span data-stu-id="839ca-105">Never use the temporary disk to store data that you need to keep.</span></span>

<span data-ttu-id="839ca-106">Si se cambia el tamaño o se selecciona **Detener (desasignar)** una máquina virtual, se puede desencadenar la colocación de la máquina virtual en un hipervisor nuevo.</span><span class="sxs-lookup"><span data-stu-id="839ca-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of the virtual machine to a new hypervisor.</span></span> <span data-ttu-id="839ca-107">Un evento de mantenimiento planificado o no planificado también puede desencadenar esta colocación.</span><span class="sxs-lookup"><span data-stu-id="839ca-107">A planned or unplanned maintenance event may also trigger this placement.</span></span> <span data-ttu-id="839ca-108">En este escenario, el disco temporal se reasignará a la primera letra de unidad disponible.</span><span class="sxs-lookup"><span data-stu-id="839ca-108">In this scenario, the temporary disk will be reassigned to the first available drive letter.</span></span> <span data-ttu-id="839ca-109">Si tiene una aplicación que necesita específicamente la unidad D:, debe seguir estos pasos para mover temporalmente el archivo pagefile.sys, adjuntar un nuevo disco de datos, asignarle la letra D y devolver el archivo pagefile.sys a la unidad temporal.</span><span class="sxs-lookup"><span data-stu-id="839ca-109">If you have an application that specifically requires the D: drive, you need to follow these steps to temporarily move the pagefile.sys, attach a new data disk and assign it the letter D and then move the pagefile.sys back to the temporary drive.</span></span> <span data-ttu-id="839ca-110">Cuando lo haya hecho, Azure no devolverá D: si la máquina virtual se desplaza a un hipervisor diferente.</span><span class="sxs-lookup"><span data-stu-id="839ca-110">Once complete, Azure will not take back the D: if the VM moves to a different hypervisor.</span></span>

<span data-ttu-id="839ca-111">Para obtener más información sobre cómo usa Azure el disco temporal, consulte [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="839ca-111">For more information about how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="attach-the-data-disk"></a><span data-ttu-id="839ca-112">Conectar el disco de datos</span><span class="sxs-lookup"><span data-stu-id="839ca-112">Attach the data disk</span></span>
<span data-ttu-id="839ca-113">En primer lugar, deberá conectar el disco de datos a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="839ca-113">First, you'll need to attach the data disk to the virtual machine.</span></span> <span data-ttu-id="839ca-114">Para hacerlo mediante el portal, consulte [How to attach a managed data disk in the Azure portal](attach-managed-disk-portal.md) (Conexión de un disco de datos administrado en Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="839ca-114">To do this using the portal, see [How to attach a managed data disk in the Azure portal](attach-managed-disk-portal.md).</span></span>

## <a name="temporarily-move-pagefilesys-to-c-drive"></a><span data-ttu-id="839ca-115">Mover temporalmente el archivo pagefile.sys a la unidad C</span><span class="sxs-lookup"><span data-stu-id="839ca-115">Temporarily move pagefile.sys to C drive</span></span>
1. <span data-ttu-id="839ca-116">Conexión a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="839ca-116">Connect to the virtual machine.</span></span> 
2. <span data-ttu-id="839ca-117">Haga clic con el botón derecho en el menú **Inicio** y seleccione **Sistema**.</span><span class="sxs-lookup"><span data-stu-id="839ca-117">Right-click the **Start** menu and select **System**.</span></span>
3. <span data-ttu-id="839ca-118">En el menú que aparece a la izquierda, seleccione **Configuración avanzada del sistema**.</span><span class="sxs-lookup"><span data-stu-id="839ca-118">In the left-hand menu, select **Advanced system settings**.</span></span>
4. <span data-ttu-id="839ca-119">En la sección **Rendimiento**, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="839ca-119">In the **Performance** section, select **Settings**.</span></span>
5. <span data-ttu-id="839ca-120">Seleccione la pestaña **Opciones avanzadas** .</span><span class="sxs-lookup"><span data-stu-id="839ca-120">Select the **Advanced** tab.</span></span>
6. <span data-ttu-id="839ca-121">En la sección **Memoria virtual**, seleccione **Cambiar**.</span><span class="sxs-lookup"><span data-stu-id="839ca-121">In the **Virtual memory** section, select **Change**.</span></span>
7. <span data-ttu-id="839ca-122">Seleccione la unidad **C**, luego haga clic en **Tamaño administrado por el sistema** y en **Establecer**.</span><span class="sxs-lookup"><span data-stu-id="839ca-122">Select the **C** drive and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="839ca-123">Seleccione la unidad **D**, luego haga clic en **Sin archivo de paginación** y, a continuación, en **Establecer**.</span><span class="sxs-lookup"><span data-stu-id="839ca-123">Select the **D** drive and then click **No paging file** and then click **Set**.</span></span>
9. <span data-ttu-id="839ca-124">Haga clic en Aplicar.</span><span class="sxs-lookup"><span data-stu-id="839ca-124">Click Apply.</span></span> <span data-ttu-id="839ca-125">Aparecerá una advertencia que indica que se debe reiniciar el equipo para que los cambios entren en vigor.</span><span class="sxs-lookup"><span data-stu-id="839ca-125">You will get a warning that the computer needs to be restarted for the changes to take affect.</span></span>
10. <span data-ttu-id="839ca-126">Reinicie la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="839ca-126">Restart the virtual machine.</span></span>

## <a name="change-the-drive-letters"></a><span data-ttu-id="839ca-127">Cambiar las letras de las unidades</span><span class="sxs-lookup"><span data-stu-id="839ca-127">Change the drive letters</span></span>
1. <span data-ttu-id="839ca-128">Una vez que se reinicia la máquina virtual, vuelva a iniciar sesión en ella.</span><span class="sxs-lookup"><span data-stu-id="839ca-128">Once the VM restarts, log back on to the VM.</span></span>
2. <span data-ttu-id="839ca-129">Haga clic en el menú **Inicio**, escriba**diskmgmt.msc** y presione Entrar.</span><span class="sxs-lookup"><span data-stu-id="839ca-129">Click the **Start** menu and type **diskmgmt.msc** and hit Enter.</span></span> <span data-ttu-id="839ca-130">Se iniciará la Administración de discos.</span><span class="sxs-lookup"><span data-stu-id="839ca-130">Disk Management will start.</span></span>
3. <span data-ttu-id="839ca-131">Haga clic con el botón derecho en **D**, la unidad de almacenamiento temporal, y seleccione **Cambiar la letra y rutas de acceso de unidad**.</span><span class="sxs-lookup"><span data-stu-id="839ca-131">Right-click on **D**, the Temporary Storage drive, and select **Change Drive Letter and Paths**.</span></span>
4. <span data-ttu-id="839ca-132">En Letra de unidad, seleccione una unidad nueva como, por ejemplo, **T** y haga clic en**Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="839ca-132">Under Drive letter, select a new drive such as **T** and then click **OK**.</span></span> 
5. <span data-ttu-id="839ca-133">Haga clic con el botón derecho en el disco de datos y seleccione **Cambiar la letra y rutas de acceso de unidad**.</span><span class="sxs-lookup"><span data-stu-id="839ca-133">Right-click on the data disk, and select **Change Drive Letter and Paths**.</span></span>
6. <span data-ttu-id="839ca-134">En Letra de unidad, seleccione la unidad **D** y haga clic en**Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="839ca-134">Under Drive letter, select drive **D** and then click **OK**.</span></span> 

## <a name="move-pagefilesys-back-to-the-temporary-storage-drive"></a><span data-ttu-id="839ca-135">Devolver el archivo pagefile.sys a la unidad de almacenamiento temporal</span><span class="sxs-lookup"><span data-stu-id="839ca-135">Move pagefile.sys back to the temporary storage drive</span></span>
1. <span data-ttu-id="839ca-136">Haga clic con el botón derecho en el menú **Inicio** y seleccione **Sistema**.</span><span class="sxs-lookup"><span data-stu-id="839ca-136">Right-click the **Start** menu and select **System**</span></span>
2. <span data-ttu-id="839ca-137">En el menú que aparece a la izquierda, seleccione **Configuración avanzada del sistema**.</span><span class="sxs-lookup"><span data-stu-id="839ca-137">In the left-hand menu, select **Advanced system settings**.</span></span>
3. <span data-ttu-id="839ca-138">En la sección **Rendimiento**, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="839ca-138">In the **Performance** section, select **Settings**.</span></span>
4. <span data-ttu-id="839ca-139">Seleccione la pestaña **Opciones avanzadas** .</span><span class="sxs-lookup"><span data-stu-id="839ca-139">Select the **Advanced** tab.</span></span>
5. <span data-ttu-id="839ca-140">En la sección **Memoria virtual**, seleccione **Cambiar**.</span><span class="sxs-lookup"><span data-stu-id="839ca-140">In the **Virtual memory** section, select **Change**.</span></span>
6. <span data-ttu-id="839ca-141">Seleccione la unidad del sistema operativo **C**, haga clic en **Sin archivo de paginación** y luego en **Establecer**.</span><span class="sxs-lookup"><span data-stu-id="839ca-141">Select the OS drive **C** and click **No paging file** and then click **Set**.</span></span>
7. <span data-ttu-id="839ca-142">Seleccione la unidad de almacenamiento temporal **T**, haga clic en **Tamaño administrado por el sistema** y, a continuación, en **Establecer**.</span><span class="sxs-lookup"><span data-stu-id="839ca-142">Select the temporary storage drive **T** and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="839ca-143">Haga clic en **Apply**.</span><span class="sxs-lookup"><span data-stu-id="839ca-143">Click **Apply**.</span></span> <span data-ttu-id="839ca-144">Aparecerá una advertencia que indica que se debe reiniciar el equipo para que los cambios entren en vigor.</span><span class="sxs-lookup"><span data-stu-id="839ca-144">You will get a warning that the computer needs to be restarted for the changes to take affect.</span></span>
9. <span data-ttu-id="839ca-145">Reinicie la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="839ca-145">Restart the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="839ca-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="839ca-146">Next steps</span></span>
* <span data-ttu-id="839ca-147">Puede aumentar el almacenamiento disponible para la máquina virtual [conectando un disco de datos adicional](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="839ca-147">You can increase the storage available to your virtual machine by [attaching a additional data disk](attach-managed-disk-portal.md).</span></span>

