---
title: aaaCapture una imagen de una VM de Linux | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocapture una imagen de una basados en Linux Azure máquina virtual (VM) creado con el modelo de implementación clásica de Hola."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="0245e-103">¿Cómo toocapture una máquina virtual de Linux clásica como imagen</span><span class="sxs-lookup"><span data-stu-id="0245e-103">How toocapture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0245e-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0245e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0245e-105">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="0245e-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="0245e-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0245e-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="0245e-107">Obtenga información acerca de cómo demasiado[realizar estos pasos con el modelo del Administrador de recursos de hello](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0245e-107">Learn how too[perform these steps using hello Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0245e-108">Este artículo muestra cómo toocapture una clásica máquina virtual de Azure (VM) ejecutan Linux como una imagen toocreate otras máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="0245e-108">This article shows you how toocapture a classic Azure virtual machine (VM) running Linux as an image toocreate other virtual machines.</span></span> <span data-ttu-id="0245e-109">Esta imagen de disco del sistema operativo hello y discos de datos acoplados toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0245e-109">This image includes hello OS disk and data disks attached toohello VM.</span></span> <span data-ttu-id="0245e-110">No incluye la configuración de red, por lo que necesita tooconfigure que cuando creas Hola otra máquina virtual desde la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="0245e-110">It doesn't include networking configuration, so you need tooconfigure that when you create hello other VM from hello image.</span></span>

<span data-ttu-id="0245e-111">Almacenes de Azure Hola imagen en **imágenes**, junto con las imágenes que ha cargado.</span><span class="sxs-lookup"><span data-stu-id="0245e-111">Azure stores hello image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="0245e-112">Para obtener más información sobre las imágenes, consulte [Acerca de las imágenes para las máquinas virtuales Linux][About Virtual Machine Images in Azure].</span><span class="sxs-lookup"><span data-stu-id="0245e-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0245e-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="0245e-113">Before you begin</span></span>
<span data-ttu-id="0245e-114">Estos pasos se supone que ya ha creado una máquina virtual de Azure mediante el modelo de implementación clásica de Hola y sistema operativo de hello configurado, incluida la conexión de los discos de datos.</span><span class="sxs-lookup"><span data-stu-id="0245e-114">These steps assume that you've already created an Azure VM using hello Classic deployment model and configured hello operating system, including attaching any data disks.</span></span> <span data-ttu-id="0245e-115">Si necesita toocreate una máquina virtual, lea [cómo tooCreate una máquina Virtual Linux][How tooCreate a Linux Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="0245e-115">If you need toocreate a VM, read [How tooCreate a Linux Virtual Machine][How tooCreate a Linux Virtual Machine].</span></span>

## <a name="capture-hello-virtual-machine"></a><span data-ttu-id="0245e-116">Captura de máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="0245e-116">Capture hello virtual machine</span></span>
1. <span data-ttu-id="0245e-117">[Conectar toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mediante un cliente de SSH de su elección.</span><span class="sxs-lookup"><span data-stu-id="0245e-117">[Connect toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="0245e-118">En la ventana de hello SSH, escriba Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="0245e-118">In hello SSH window, type hello following command.</span></span> <span data-ttu-id="0245e-119">Hola de salida de `waagent` puede variar ligeramente según la versión de Hola de esta utilidad:</span><span class="sxs-lookup"><span data-stu-id="0245e-119">hello output from `waagent` may vary slightly depending on hello version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="0245e-120">Hola comando anterior intentos de sistema de hello tooclean y que sea adecuado para reaprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="0245e-120">hello preceding command attempts tooclean hello system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="0245e-121">Esta operación realiza Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="0245e-121">This operation performs hello following tasks:</span></span>

   * <span data-ttu-id="0245e-122">Quita las claves de host SSH (si Provisioning.RegenerateSshHostKeyPair es 'y' en el archivo de configuración de hello)</span><span class="sxs-lookup"><span data-stu-id="0245e-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="0245e-123">Borra la configuración de Nameserver en /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="0245e-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="0245e-124">Quita hello `root` contraseña de usuario de/etcetera/instantáneas (si Provisioning.DeleteRootPassword es 'y' en el archivo de configuración de hello)</span><span class="sxs-lookup"><span data-stu-id="0245e-124">Removes hello `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="0245e-125">Quita concesiones del cliente de DHCP en caché</span><span class="sxs-lookup"><span data-stu-id="0245e-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="0245e-126">Restablece toolocalhost.localdomain de nombre de host</span><span class="sxs-lookup"><span data-stu-id="0245e-126">Resets host name toolocalhost.localdomain</span></span>
   * <span data-ttu-id="0245e-127">Elimina la última cuenta de usuario aprovisionado hello (obtenido de /var/lib/waagent) **y los datos asociados**.</span><span class="sxs-lookup"><span data-stu-id="0245e-127">Deletes hello last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="0245e-128">Desaprovisionamiento elimina archivos y datos demasiado "generalizar" hello imagen.</span><span class="sxs-lookup"><span data-stu-id="0245e-128">Deprovisioning deletes files and data too"generalize" hello image.</span></span> <span data-ttu-id="0245e-129">Solo se ejecute este comando en una máquina virtual que piensa toocapture como una nueva plantilla de imagen.</span><span class="sxs-lookup"><span data-stu-id="0245e-129">Only run this command on a VM that you intend toocapture as a new image template.</span></span> <span data-ttu-id="0245e-130">No se garantiza dicha imagen Hola se borra de toda la información confidencial o es adecuada para las partes de toothird de redistribución.</span><span class="sxs-lookup"><span data-stu-id="0245e-130">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution toothird parties.</span></span>

3. <span data-ttu-id="0245e-131">Tipo de **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="0245e-131">Type **y** toocontinue.</span></span> <span data-ttu-id="0245e-132">Puede agregar hello `-force` parámetro tooavoid este paso de confirmación.</span><span class="sxs-lookup"><span data-stu-id="0245e-132">You can add hello `-force` parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="0245e-133">Tipo de **Exit** cliente de SSH de tooclose Hola.</span><span class="sxs-lookup"><span data-stu-id="0245e-133">Type **Exit** tooclose hello SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0245e-134">Hello pasos restantes se supone que ya está [instalado hello Azure CLI](../../../cli-install-nodejs.md) en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="0245e-134">hello remaining steps assume you have already [installed hello Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="0245e-135">También es posible Hola todos los pasos en hello [portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0245e-135">All hello following steps can also be done in hello [Azure portal](http://portal.azure.com).</span></span>

5. <span data-ttu-id="0245e-136">En el equipo cliente, abra CLI de Azure y el inicio de sesión tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="0245e-136">From your client computer, open Azure CLI and login tooyour Azure subscription.</span></span> <span data-ttu-id="0245e-137">Para obtener más información, lea [conectarse tooan suscripción de Azure desde hello Azure CLI](../../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="0245e-137">For details, read [Connect tooan Azure subscription from hello Azure CLI](../../../xplat-cli-connect.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="0245e-138">Hola portal de Azure, inicie sesión en el portal de toohello.</span><span class="sxs-lookup"><span data-stu-id="0245e-138">In hello Azure portal, log in toohello portal.</span></span>

6. <span data-ttu-id="0245e-139">Asegúrese de que está en modo de administración de servicios:</span><span class="sxs-lookup"><span data-stu-id="0245e-139">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="0245e-140">Apagar máquina virtual que ya se desaprovisiona Hola.</span><span class="sxs-lookup"><span data-stu-id="0245e-140">Shut down hello VM that is already deprovisioned.</span></span> <span data-ttu-id="0245e-141">Hello en el ejemplo siguiente se cierra Hola máquina virtual denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="0245e-141">hello following example shuts down hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```
   <span data-ttu-id="0245e-142">Si es necesario, puede ver una lista Hola todas las máquinas virtuales se crea en su suscripción mediante`azure vm list`</span><span class="sxs-lookup"><span data-stu-id="0245e-142">If needed, you can view a list all hello VMs created in your subscription by using `azure vm list`</span></span>

   > [!NOTE]
   > <span data-ttu-id="0245e-143">Si usas Hola portal de Azure, seleccione Hola máquina virtual y haga clic en **detener** apagar VM Hola.</span><span class="sxs-lookup"><span data-stu-id="0245e-143">If you're using hello Azure portal, select hello VM and click **Stop** to shut down hello VM.</span></span>

8. <span data-ttu-id="0245e-144">Cuando se detiene Hola VM, capture la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="0245e-144">When hello VM is stopped, capture hello image.</span></span> <span data-ttu-id="0245e-145">Hola siguientes capturas de ejemplo Hola máquina virtual denominada `myVM` y crea una imagen generalizada denominada `myNewVM`:</span><span class="sxs-lookup"><span data-stu-id="0245e-145">hello following example captures hello VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="0245e-146">Hola `-t` subcomando eliminaciones Hola máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="0245e-146">hello `-t` subcommand deletes hello original virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0245e-147">Hola portal de Azure, puede capturar una imagen seleccionando **imagen** desde el menú del concentrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="0245e-147">In hello Azure portal, you can capture an image by selecting **Image** from hello hub menu.</span></span> <span data-ttu-id="0245e-148">Necesita hello toosupply siguiendo la información de imagen de Hola: nombre, grupo de recursos, ubicación, tipo de sistema operativo y ruta de acceso de almacenamiento blob.</span><span class="sxs-lookup"><span data-stu-id="0245e-148">You need toosupply hello following information for hello image: name, resource group, location, operating system type, and storage blob path.</span></span>

9. <span data-ttu-id="0245e-149">Hola nueva imagen está ahora disponible en hello lista de imágenes que se puede usa tooconfigure cualquier nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0245e-149">hello new image is now available in hello list of images that can be used tooconfigure any new VM.</span></span> <span data-ttu-id="0245e-150">Puede verlo con el comando hello:</span><span class="sxs-lookup"><span data-stu-id="0245e-150">You can view it with hello command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="0245e-151">En hello [portal de Azure](http://portal.azure.com), Hola nueva imagen aparece en hello **imágenes de máquina virtual (clásica)** que pertenece toohello **proceso** servicios.</span><span class="sxs-lookup"><span data-stu-id="0245e-151">On hello [Azure portal](http://portal.azure.com), hello new image appears in hello **VM images (classic)** that belongs toohello **Compute** services.</span></span> <span data-ttu-id="0245e-152">Puede tener acceso a **imágenes de máquina virtual (clásica)** haciendo clic en _más servicios_ final Hola de hello Azure servicio lista y, a continuación, busca en hello **proceso** servicios.</span><span class="sxs-lookup"><span data-stu-id="0245e-152">You can access **VM images (classic)** by clicking _More services_ at hello bottom of hello Azure service list, and then looking in hello **Compute** services.</span></span>   

   ![Captura correcta de la imagen](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="0245e-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0245e-154">Next steps</span></span>
<span data-ttu-id="0245e-155">imagen de Hello es toocreate toobe listo usa máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="0245e-155">hello image is ready toobe used toocreate VMs.</span></span> <span data-ttu-id="0245e-156">Puede usar el comando de CLI de Azure de hello `azure vm create` y nombre de la imagen de Hola de alimentación que creó.</span><span class="sxs-lookup"><span data-stu-id="0245e-156">You can use hello Azure CLI command `azure vm create` and supply hello image name you created.</span></span> <span data-ttu-id="0245e-157">Para obtener más información, consulte [Using Hola CLI de Azure con el modelo de implementación clásica](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="0245e-157">For more information, see [Using hello Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="0245e-158">O bien, usar hello [portal de Azure](http://portal.azure.com) toocreate una máquina virtual personalizada mediante el uso de hello **imagen** método y seleccionando hello de la imagen que ha creado.</span><span class="sxs-lookup"><span data-stu-id="0245e-158">Alternatively, use hello [Azure portal](http://portal.azure.com) toocreate a custom VM by using hello **Image** method and selecting hello image you created.</span></span> <span data-ttu-id="0245e-159">Para obtener más información, consulte [cómo tooCreate una VM personalizada][How tooCreate a Custom Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="0245e-159">For more information, see [How tooCreate a Custom VM][How tooCreate a Custom Virtual Machine].</span></span>

<span data-ttu-id="0245e-160">**Consulte también:**[Guía de usuario del Agente de Linux de Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0245e-160">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
