---
title: "Conexión de un disco a una máquina virtual de Azure clásico | Microsoft Docs"
description: "Conecte un disco de datos a una máquina virtual de Windows creada con el modelo de implementación clásica e inicialícelo."
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
ms.openlocfilehash: 087d5cda354f6e1780bddd3725859444177abd16
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="attach-a-data-disk-to-a-windows-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="6d26a-103">Conecte un disco de datos a una máquina virtual de Windows creada con el modelo de implementación clásica</span><span class="sxs-lookup"><span data-stu-id="6d26a-103">Attach a data disk to a Windows virtual machine created with the classic deployment model</span></span>
<!--
Refernce article:
    If you want to use the new portal, see [How to attach a data disk to a Windows VM in the Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="6d26a-104">En este artículo se muestra cómo conectar discos nuevos y existentes creados con el modelo de implementación clásica a una máquina virtual Windows mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6d26a-104">This article shows you how to attach new and existing disks created with the Classic deployment model to a Windows virtual machine using the Azure portal.</span></span>

<span data-ttu-id="6d26a-105">También puede [adjuntar un disco de datos a una máquina virtual Linux en el Portal de Azure](../../linux/attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6d26a-105">You can also [attach a data disk to a Linux VM in the Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="6d26a-106">Antes de conectar un disco, revise estas sugerencias:</span><span class="sxs-lookup"><span data-stu-id="6d26a-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="6d26a-107">El tamaño de la máquina virtual controla cuántos discos de datos puede conectar.</span><span class="sxs-lookup"><span data-stu-id="6d26a-107">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="6d26a-108">Para obtener más información, consulte [Tamaños de máquinas virtuales](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d26a-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="6d26a-109">Para usar Premium Storage, necesita una máquina virtual de la serie DS o GS.</span><span class="sxs-lookup"><span data-stu-id="6d26a-109">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="6d26a-110">Puede utilizar discos de cuentas de almacenamiento premium y estándar con estas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6d26a-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="6d26a-111">Almacenamiento premium está disponible en determinadas regiones.</span><span class="sxs-lookup"><span data-stu-id="6d26a-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="6d26a-112">Para obtener más información, consulte [Almacenamiento Premium: Almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="6d26a-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="6d26a-113">Para un disco nuevo, no es necesario crearlo en primer lugar porque Azure lo crea cuando lo conecta.</span><span class="sxs-lookup"><span data-stu-id="6d26a-113">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="6d26a-114">También puede [conectar un disco de datos mediante Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6d26a-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6d26a-115">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6d26a-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-the-virtual-machine"></a><span data-ttu-id="6d26a-116">Búsqueda de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6d26a-116">Find the virtual machine</span></span>
1. <span data-ttu-id="6d26a-117">Inicie sesión en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6d26a-117">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6d26a-118">Seleccione la máquina virtual en el recurso que aparece en el panel.</span><span class="sxs-lookup"><span data-stu-id="6d26a-118">Select the virtual machine from the resource listed on the dashboard.</span></span>
3. <span data-ttu-id="6d26a-119">En el panel izquierdo, en **Configuración**, haga clic en **Discos**.</span><span class="sxs-lookup"><span data-stu-id="6d26a-119">In the left pane under **Settings**, click **Disks**.</span></span>

    ![Abrir configuración de disco](./media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="6d26a-121">Continúe siguiendo las instrucciones para conectar un [nuevo disco](#option-1-attach-a-new-disk) o un [disco existente](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="6d26a-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="6d26a-122">Opción 1: adjunte e inicialice un disco nuevo</span><span class="sxs-lookup"><span data-stu-id="6d26a-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="6d26a-123">En la hoja **Discos**, haga clic en **Adjuntar nuevo**.</span><span class="sxs-lookup"><span data-stu-id="6d26a-123">On the **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="6d26a-124">Revise la configuración predeterminada, actualice según sea necesario y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6d26a-124">Review the default settings, update as necessary, and then click **OK**.</span></span>

   ![Revisar configuración de disco](./media/attach-disk/attach-new.png)

3. <span data-ttu-id="6d26a-126">Una vez que Azure crea el disco y lo adjunta a la máquina virtual, el nuevo disco aparece en la configuración de disco de la máquina virtual en el apartado **Discos de datos**.</span><span class="sxs-lookup"><span data-stu-id="6d26a-126">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="6d26a-127">Inicio de un nuevo disco de datos</span><span class="sxs-lookup"><span data-stu-id="6d26a-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="6d26a-128">Conexión a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6d26a-128">Connect to the virtual machine.</span></span> <span data-ttu-id="6d26a-129">Para obtener instrucciones, consulte [Conexión a una máquina virtual de Azure donde se ejecuta Windows Server e inicio de sesión en ella](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d26a-129">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="6d26a-130">Después de iniciar sesión en la máquina virtual, abra el **Administrador del servidor**.</span><span class="sxs-lookup"><span data-stu-id="6d26a-130">After you log on to the virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="6d26a-131">En el panel izquierdo, seleccione **Servicios de archivos y almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="6d26a-131">In the left pane, select **File and Storage Services**.</span></span>

    ![Abrir Administrador de servidores](../media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="6d26a-133">Seleccione **Discos**.</span><span class="sxs-lookup"><span data-stu-id="6d26a-133">Select **Disks**.</span></span>
4. <span data-ttu-id="6d26a-134">En la sección **Discos** aparecen todos los discos.</span><span class="sxs-lookup"><span data-stu-id="6d26a-134">The **Disks** section lists the disks.</span></span> <span data-ttu-id="6d26a-135">A menudo, una máquina virtual tiene los discos 0, 1 y 2.</span><span class="sxs-lookup"><span data-stu-id="6d26a-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="6d26a-136">El disco 0 es el del sistema operativo, el 1 es el disco temporal y el 2 es el disco de datos que acaba de conectar a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6d26a-136">Disk 0 is the operating system disk, disk 1 is the temporary disk, and disk 2 is the data disk newly attached to the virtual machine.</span></span> <span data-ttu-id="6d26a-137">El disco de datos muestra la partición como **Desconocida**.</span><span class="sxs-lookup"><span data-stu-id="6d26a-137">The data disk lists the Partition as **Unknown**.</span></span>

 <span data-ttu-id="6d26a-138">Haga clic con el botón derecho en el disco y seleccione **Inicializar**.</span><span class="sxs-lookup"><span data-stu-id="6d26a-138">Right-click the disk and select **Initialize**.</span></span>

5. <span data-ttu-id="6d26a-139">Se le notificará que se borrarán todos los datos cuando se inicializa el disco.</span><span class="sxs-lookup"><span data-stu-id="6d26a-139">You're notified that all data will be erased when the disk is initialized.</span></span> <span data-ttu-id="6d26a-140">Haga clic en **Sí** para confirmar la advertencia e inicializar el disco.</span><span class="sxs-lookup"><span data-stu-id="6d26a-140">Click **Yes** to acknowledge the warning and initialize the disk.</span></span> <span data-ttu-id="6d26a-141">Una vez que se complete el proceso, la partición aparecerá como **GPT**.</span><span class="sxs-lookup"><span data-stu-id="6d26a-141">Once complete, the partition will be listed as **GPT**.</span></span> <span data-ttu-id="6d26a-142">Vuelva a hacer clic con el botón derecho en el disco y seleccione **Nuevo volumen**.</span><span class="sxs-lookup"><span data-stu-id="6d26a-142">Right-click the disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="6d26a-143">Complete el asistente usando los valores predeterminados que se proporcionan.</span><span class="sxs-lookup"><span data-stu-id="6d26a-143">Complete the wizard using the default values.</span></span> <span data-ttu-id="6d26a-144">Cuando haya finalizado el asistente, la sección **Volúmenes** mostrará el nuevo volumen.</span><span class="sxs-lookup"><span data-stu-id="6d26a-144">When the wizard is done, the **Volumes** section lists the new volume.</span></span> <span data-ttu-id="6d26a-145">El disco está ahora conectado y listo para almacenar los datos.</span><span class="sxs-lookup"><span data-stu-id="6d26a-145">The disk is now online and ready to store data.</span></span>

    ![Volumen inicializado correctamente](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="6d26a-147">Opción 2: Conectar un disco existente</span><span class="sxs-lookup"><span data-stu-id="6d26a-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="6d26a-148">En la hoja **Discos**, haga clic en **Adjuntar existente**.</span><span class="sxs-lookup"><span data-stu-id="6d26a-148">On the **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="6d26a-149">En **Adjuntar un disco existente**, haga clic en **Ubicación**.</span><span class="sxs-lookup"><span data-stu-id="6d26a-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![Conectar disco existente](./media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="6d26a-151">En **Cuentas de almacenamiento**, seleccione la cuenta y el contenedor que incluyen el archivo .vhd.</span><span class="sxs-lookup"><span data-stu-id="6d26a-151">Under **Storage accounts**, select the account and container that holds the .vhd file.</span></span>

   ![Buscar ubicación de VHD](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="6d26a-153">Seleccione el archivo .vhd.</span><span class="sxs-lookup"><span data-stu-id="6d26a-153">Select the .vhd file.</span></span>
5. <span data-ttu-id="6d26a-154">En **Adjuntar un disco existente**, el archivo que acaba de seleccionar aparece en **Archivo VHD**.</span><span class="sxs-lookup"><span data-stu-id="6d26a-154">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="6d26a-155">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6d26a-155">Click **OK**.</span></span>
6. <span data-ttu-id="6d26a-156">Una vez que Azure adjunta el disco a la máquina virtual,este aparece en la configuración del disco de la máquina virtual en el apartado **Discos de datos**.</span><span class="sxs-lookup"><span data-stu-id="6d26a-156">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="6d26a-157">Uso de TRIM con el almacenamiento estándar</span><span class="sxs-lookup"><span data-stu-id="6d26a-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="6d26a-158">Si utiliza almacenamiento estándar (HDD), debe habilitar TRIM.</span><span class="sxs-lookup"><span data-stu-id="6d26a-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="6d26a-159">TRIM descarta los bloques sin utilizar del disco, por lo que solo se le facturará el almacenamiento que utiliza realmente.</span><span class="sxs-lookup"><span data-stu-id="6d26a-159">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="6d26a-160">Puede ahorrar costos si usa TRIM, además de los bloques sin utilizar por eliminar archivos de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="6d26a-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="6d26a-161">Puede ejecutar este comando para comprobar la configuración de TRIM.</span><span class="sxs-lookup"><span data-stu-id="6d26a-161">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="6d26a-162">Abra un símbolo del sistema en su máquina virtual de Windows y escriba:</span><span class="sxs-lookup"><span data-stu-id="6d26a-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="6d26a-163">Si el comando devuelve 0, significa que TRIM está habilitada correctamente.</span><span class="sxs-lookup"><span data-stu-id="6d26a-163">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="6d26a-164">Si devuelve 1, ejecute el siguiente comando para habilitar TRIM:</span><span class="sxs-lookup"><span data-stu-id="6d26a-164">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="6d26a-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6d26a-165">Next steps</span></span>
<span data-ttu-id="6d26a-166">Si la aplicación debe usar la unidad D: para almacenar datos, puede [cambiar la letra de la unidad del disco temporal de Windows](../../virtual-machines-windows-change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="6d26a-166">If your application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6d26a-167">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="6d26a-167">Additional resources</span></span>
[<span data-ttu-id="6d26a-168">Acerca de los discos y los discos duros virtuales para máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="6d26a-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)
