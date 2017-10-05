---
title: "Captura de una imagen de una máquina virtual Windows de Azure | Microsoft Docs"
description: "Capture una imagen de una máquina virtual Windows de Azure creada con el modelo de implementación clásica."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 6032263848c469ce2f416306e5c91c29f4cb30e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="bd0a0-103">Capture una imagen de una máquina virtual Windows de Azure creada con el modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-103">Capture an image of an Azure Windows virtual machine created with the classic deployment model.</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bd0a0-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bd0a0-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bd0a0-105">En este artículo se trata el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="bd0a0-106">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="bd0a0-107">Para obtener información del modelo de Resource Manager, vea [Capturar una imagen administrada de una máquina virtual generalizada en Azure](../capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="bd0a0-107">For Resource Manager model information, see [Capture a managed image of a generalized VM in Azure](../capture-image-resource.md).</span></span>

<span data-ttu-id="bd0a0-108">En este artículo se muestra cómo puede capturar una máquina virtual de Azure con Windows para usarla como imagen en la creación de otras máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-108">This article shows you how to capture an Azure virtual machine running Windows so you can use it as an image to create other virtual machines.</span></span> <span data-ttu-id="bd0a0-109">Esta imagen incluye el disco del sistema operativo y los discos de datos que están conectados a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-109">This image includes the operating system disk and any data disks that are attached to the virtual machine.</span></span> <span data-ttu-id="bd0a0-110">No incluye configuraciones de red, por lo que deberá establecerlas cuando cree las otras máquinas virtuales que usan la imagen.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-110">It doesn't include networking configurations, so you'll need to set up network configurations when you create the other virtual machines that use the image.</span></span>

<span data-ttu-id="bd0a0-111">Azure almacena la imagen en **Imágenes de la VM (clásico)**, un servicio de **proceso** que se muestra cuando aparecen todos los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-111">Azure stores the image under **VM images (classic)**, a **Compute** service that is listed when you view all the Azure services.</span></span> <span data-ttu-id="bd0a0-112">Este es el mismo lugar donde se almacenan las imágenes que se han cargado.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-112">This is the same place where any images you've uploaded are stored.</span></span> <span data-ttu-id="bd0a0-113">Para obtener más información acerca de las imágenes, vea [Acerca de las imágenes para las máquinas virtuales](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd0a0-113">For details about images, see [About images for virtual machines](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bd0a0-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="bd0a0-114">Before you begin</span></span>
<span data-ttu-id="bd0a0-115">Para seguir estos pasos se supone que ya ha creado un máquina virtual Azure y ha configurado el sistema operativo, incluida la anexión de cualquier disco de datos.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-115">These steps assume that you've already created an Azure virtual machine and configured the operating system, including attaching any data disks.</span></span> <span data-ttu-id="bd0a0-116">Si no lo ha hecho todavía, consulte los siguientes artículos para obtener información sobre la creación y preparación de la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="bd0a0-116">If you haven't done this yet, see the following articles for information on creating and preparing the virtual machine:</span></span>

* [<span data-ttu-id="bd0a0-117">Cree una máquina virtual desde una imagen</span><span class="sxs-lookup"><span data-stu-id="bd0a0-117">Create a virtual machine from an image</span></span>](createportal.md)
* [<span data-ttu-id="bd0a0-118">Acoplamiento de un disco de datos a una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bd0a0-118">How to attach a data disk to a virtual machine</span></span>](attach-disk.md)
* <span data-ttu-id="bd0a0-119">Asegúrese de que los roles de servidor admiten Sysprep.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-119">Make sure the server roles are supported with Sysprep.</span></span> <span data-ttu-id="bd0a0-120">Para más información, consulte [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)(Compatibilidad de Sysprep con roles de servidor).</span><span class="sxs-lookup"><span data-stu-id="bd0a0-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

> [!WARNING]
> <span data-ttu-id="bd0a0-121">Este proceso elimina la máquina virtual original después de capturarla.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-121">This process deletes the original virtual machine after it's captured.</span></span>
>
>

<span data-ttu-id="bd0a0-122">Antes de capturar una imagen de una máquina virtual de Azure, se recomienda hacer una copia de seguridad de la máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-122">Prior to capturing an image of an Azure virtual machine, it is recommended the target virtual machine be backed up.</span></span> <span data-ttu-id="bd0a0-123">Esto se puede hacer mediante Copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-123">Azure virtual machines can be backed up using Azure Backup.</span></span> <span data-ttu-id="bd0a0-124">Para obtener más información, consulte [Copia de seguridad de máquinas virtuales de Azure](../../../backup/backup-azure-vms.md).</span><span class="sxs-lookup"><span data-stu-id="bd0a0-124">For details, see [Back up Azure virtual machines](../../../backup/backup-azure-vms.md).</span></span> <span data-ttu-id="bd0a0-125">Hay otras soluciones disponibles de socios certificados.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-125">Other solutions are available from certified partners.</span></span> <span data-ttu-id="bd0a0-126">Para averiguar lo que está actualmente disponible, busque Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-126">To find out what’s currently available, search the Azure Marketplace.</span></span>

## <a name="capture-the-virtual-machine"></a><span data-ttu-id="bd0a0-127">Captura de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bd0a0-127">Capture the virtual machine</span></span>
1. <span data-ttu-id="bd0a0-128">En [Azure Portal](http://portal.azure.com), **conecte** con la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-128">In the [Azure portal](http://portal.azure.com), **Connect** to the virtual machine.</span></span> <span data-ttu-id="bd0a0-129">Para obtener instrucciones, consulte [Inicio de sesión en una máquina virtual con Windows Server][How to sign in to a virtual machine running Windows Server].</span><span class="sxs-lookup"><span data-stu-id="bd0a0-129">For instructions, see [How to sign in to a virtual machine running Windows Server][How to sign in to a virtual machine running Windows Server].</span></span>
2. <span data-ttu-id="bd0a0-130">Abra una ventana de símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-130">Open a Command Prompt window as an administrator.</span></span>
3. <span data-ttu-id="bd0a0-131">Cambie el directorio a `%windir%\system32\sysprep`y después ejecute sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-131">Change the directory to `%windir%\system32\sysprep`, and then run sysprep.exe.</span></span>
4. <span data-ttu-id="bd0a0-132">Aparecerá el cuadro de diálogo **Herramienta de preparación del sistema** .</span><span class="sxs-lookup"><span data-stu-id="bd0a0-132">The **System Preparation Tool** dialog box appears.</span></span> <span data-ttu-id="bd0a0-133">Haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bd0a0-133">Do the following:</span></span>

   * <span data-ttu-id="bd0a0-134">En **Acción de limpieza del sistema**, seleccione **Iniciar la configuración rápida (OOBE) del sistema**  y asegúrese de que la opción **Generalizar** está marcada.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-134">In **System Cleanup Action**, select **Enter System Out-of-Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span> <span data-ttu-id="bd0a0-135">Para obtener más información sobre el uso de Sysprep, consulte [Uso de Sysprep: Introducción][How to Use Sysprep: An Introduction].</span><span class="sxs-lookup"><span data-stu-id="bd0a0-135">For more information about using Sysprep, see [How to Use Sysprep: An Introduction][How to Use Sysprep: An Introduction].</span></span>
   * <span data-ttu-id="bd0a0-136">En **Opciones de apagado**, seleccione **Apagar**.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-136">In **Shutdown Options**, select **Shutdown**.</span></span>
   * <span data-ttu-id="bd0a0-137">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-137">Click **OK**.</span></span>

   ![Ejecute Sysprep](./media/capture-image/SysprepGeneral.png)
5. <span data-ttu-id="bd0a0-139">Sysprep apaga la máquina virtual, lo que cambia su estado en Azure Portal a **Detenido**.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-139">Sysprep shuts down the virtual machine, which changes the status of the virtual machine in the Azure portal to **Stopped**.</span></span>
6. <span data-ttu-id="bd0a0-140">En Azure Portal, haga clic en **Máquinas virtuales (clásico)** y seleccione las máquinas virtuales que desea capturar.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-140">In the Azure portal, click **Virtual Machines (classic)** and select the virtual machine you want to capture.</span></span> <span data-ttu-id="bd0a0-141">El grupo **Imágenes de la VM (clásico)** aparece en **Proceso** en la vista de **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-141">The **VM images (classic)** group is listed under **Compute** when you view **More services**.</span></span>

7. <span data-ttu-id="bd0a0-142">En la barra de comandos, haga clic en **Capturar**.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-142">On the command bar, click **Capture**.</span></span>

   ![Capture la máquina virtual](./media/capture-image/CaptureVM.png)

   <span data-ttu-id="bd0a0-144">Aparece el cuadro de diálogo **Capturar la máquina virtual** .</span><span class="sxs-lookup"><span data-stu-id="bd0a0-144">The **Capture the Virtual Machine** dialog box appears.</span></span>

8. <span data-ttu-id="bd0a0-145">En **Nombre de imagen**, escriba un nombre para la nueva imagen.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-145">In **Image name**, type a name for the new image.</span></span> <span data-ttu-id="bd0a0-146">En **Etiqueta de imagen**, escriba una etiqueta para la nueva imagen.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-146">In **Image label**, type a label for the new image.</span></span>

9. <span data-ttu-id="bd0a0-147">Haga clic en **I've run Sysprep on the virtual machine** (He ejecutado Sysprep en la máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="bd0a0-147">Click **I've run Sysprep on the virtual machine**.</span></span> <span data-ttu-id="bd0a0-148">Esta casilla hace referencia a las acciones realizadas con Sysprep en los pasos 3 a 5.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-148">This checkbox refers to the actions with Sysprep in steps 3-5.</span></span> <span data-ttu-id="bd0a0-149">Una imagen _debe_ generalizarse con la ejecución de Sysprep antes de agregar una imagen de Windows Server al conjunto de imágenes personalizadas.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-149">An image _must_ be generalized by running Sysprep before you add a Windows Server image to your set of custom images.</span></span>

10. <span data-ttu-id="bd0a0-150">Una vez completada la captura, la nueva imagen está disponible en el contenedor **Marketplace**, **Proceso** e **Imágenes de la VM (clásico)**.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-150">Once the capture completes, the new image becomes available in the **Marketplace**, in the **Compute**, **VM images (classic)** container.</span></span>

    ![Captura correcta de la imagen](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="bd0a0-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bd0a0-152">Next steps</span></span>
<span data-ttu-id="bd0a0-153">La imagen está lista para usarse para crear máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-153">The image is ready to be used to create virtual machines.</span></span> <span data-ttu-id="bd0a0-154">En este caso, necesita crear una máquina virtual; para ello, seleccione el elemento de menú **Más servicios** en la parte inferior del menú de servicios y luego seleccione **Imágenes de la VM (clásico)** en el grupo **Proceso**.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-154">To do this, you'll create a virtual machine by selecting the **More services** menu item at the bottom of the services menu, then **VM images (classic)** in the **Compute** group.</span></span> <span data-ttu-id="bd0a0-155">Para obtener instrucciones, consulte [Creación de una máquina virtual desde una imagen](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="bd0a0-155">For instructions, see [Create a virtual machine from an image](createportal.md).</span></span>

[How to sign in to a virtual machine running Windows Server]:connect-logon.md
[How to Use Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[The virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of the virtual machine]: ./media/capture-image/CaptureVM.png
[Enter the image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use the captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
