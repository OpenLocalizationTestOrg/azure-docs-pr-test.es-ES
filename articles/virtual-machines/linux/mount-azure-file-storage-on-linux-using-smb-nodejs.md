---
title: "almacenamiento de archivos de Azure en máquinas virtuales de Linux mediante el uso de SMB con Azure CLI 1.0 aaaMount | Documentos de Microsoft"
description: "¿Cómo toomount almacenamiento de archivos de Azure en máquinas virtuales de Linux mediante el uso de SMB"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: 14a4224228cadb0ae2f05e8e5c8022ee84f138a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a><span data-ttu-id="e85cb-103">Montaje de Azure File Storage en VM Linux mediante SMB con la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e85cb-103">Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0</span></span>

<span data-ttu-id="e85cb-104">Este artículo muestra cómo toomount almacenamiento de archivos de Azure en una VM de Linux mediante el uso de Hola protocolo de bloque de mensajes del servidor (SMB).</span><span class="sxs-lookup"><span data-stu-id="e85cb-104">This article shows how toomount Azure File storage on a Linux VM by using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="e85cb-105">Almacenamiento de archivos ofrece recursos compartidos de archivos en la nube de Hola a través del protocolo SMB estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="e85cb-105">File storage offers file shares in hello cloud via hello standard SMB protocol.</span></span> <span data-ttu-id="e85cb-106">Hola requisitos son:</span><span class="sxs-lookup"><span data-stu-id="e85cb-106">hello requirements are:</span></span>

* <span data-ttu-id="e85cb-107">Una [cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="e85cb-107">An [Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* [<span data-ttu-id="e85cb-108">Archivos de clave pública y privada Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="e85cb-108">Secure Shell (SSH) public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="cli-versions-toouse"></a><span data-ttu-id="e85cb-109">Toouse de versiones CLI</span><span class="sxs-lookup"><span data-stu-id="e85cb-109">CLI versions toouse</span></span>
<span data-ttu-id="e85cb-110">Puede completar la tarea hello mediante uno de hello después de versiones de la interfaz de línea de comandos (CLI):</span><span class="sxs-lookup"><span data-stu-id="e85cb-110">You can complete hello task by using one of hello following command-line interface (CLI) versions:</span></span>

- <span data-ttu-id="e85cb-111">[Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="e85cb-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e85cb-112">[Azure 2.0 CLI](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="e85cb-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)- our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="e85cb-113">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="e85cb-113">Quick commands</span></span>
<span data-ttu-id="e85cb-114">tarea de hello tooaccomplish rápidamente, siga los pasos de hello en esta sección.</span><span class="sxs-lookup"><span data-stu-id="e85cb-114">tooaccomplish hello task quickly, follow hello steps in this section.</span></span> <span data-ttu-id="e85cb-115">Para obtener más información y el contexto, comienzan en hello ["Tutorial detallado"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) sección.</span><span class="sxs-lookup"><span data-stu-id="e85cb-115">For more detailed information and context, begin at hello ["Detailed walkthrough"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e85cb-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e85cb-116">Prerequisites</span></span>
* <span data-ttu-id="e85cb-117">Un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e85cb-117">A resource group</span></span>
* <span data-ttu-id="e85cb-118">Una red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="e85cb-118">An Azure virtual network</span></span>
* <span data-ttu-id="e85cb-119">Un grupo de seguridad de red con un SSH entrante</span><span class="sxs-lookup"><span data-stu-id="e85cb-119">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="e85cb-120">Una subred</span><span class="sxs-lookup"><span data-stu-id="e85cb-120">A subnet</span></span>
* <span data-ttu-id="e85cb-121">Una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="e85cb-121">An Azure storage account</span></span>
* <span data-ttu-id="e85cb-122">Claves de cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="e85cb-122">Azure storage account keys</span></span>
* <span data-ttu-id="e85cb-123">Un recurso compartido de Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="e85cb-123">An Azure File storage share</span></span>
* <span data-ttu-id="e85cb-124">Una VM Linux</span><span class="sxs-lookup"><span data-stu-id="e85cb-124">A Linux VM</span></span>

<span data-ttu-id="e85cb-125">Reemplace los ejemplos por su propia configuración.</span><span class="sxs-lookup"><span data-stu-id="e85cb-125">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="e85cb-126">Cree un directorio de montaje local Hola</span><span class="sxs-lookup"><span data-stu-id="e85cb-126">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="e85cb-127">Hola archivo almacenamiento SMB recurso compartido toohello montaje punto de montaje</span><span class="sxs-lookup"><span data-stu-id="e85cb-127">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="e85cb-128">Conservar el montaje de hello tras un reinicio.</span><span class="sxs-lookup"><span data-stu-id="e85cb-128">Persist hello mount after a reboot</span></span>
<span data-ttu-id="e85cb-129">Agregar Hola siguen demasiado`/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="e85cb-129">Add hello following line too`/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="e85cb-130">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="e85cb-130">Detailed walkthrough</span></span>

<span data-ttu-id="e85cb-131">Almacenamiento de archivos ofrece recursos compartidos de archivos en la nube de Hola que utilizan el protocolo SMB estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="e85cb-131">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="e85cb-132">Con la versión más reciente de Hola de almacenamiento de archivos, también se puede montar un recurso compartido de archivos desde cualquier sistema operativo que admite SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="e85cb-132">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="e85cb-133">Cuando se usa un montaje SMB en Linux, obtendrá las copias de seguridad fácil tooa robustas y permanente archivado ubicación de almacenamiento que es compatible con un SLA.</span><span class="sxs-lookup"><span data-stu-id="e85cb-133">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="e85cb-134">Mover archivos de un montaje SMB tooan de máquina virtual que se hospeda en el almacenamiento de archivos es que una excelente manera toodebug registros.</span><span class="sxs-lookup"><span data-stu-id="e85cb-134">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="e85cb-135">Esto es así porque Hola recurso compartido SMB mismo se puede montar localmente tooyour Mac, Linux o Windows estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e85cb-135">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="e85cb-136">SMB no es la mejor solución para la transmisión por secuencias Linux de Hola o registros de aplicación en tiempo real, porque Hola protocolo SMB no se generan toohandle tales derechos de registro pesada.</span><span class="sxs-lookup"><span data-stu-id="e85cb-136">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="e85cb-137">Una herramienta de nivel de registro unificado dedicada como Fluentd sería una opción mejor que SMB para recopilar la salida de registro de la aplicación y Linux.</span><span class="sxs-lookup"><span data-stu-id="e85cb-137">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="e85cb-138">Para este tutorial detallado, creamos requisitos previos de hello necesario toofirst crear recurso compartido de almacenamiento de archivos de hello y, a continuación, monte a través de SMB en una VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="e85cb-138">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="e85cb-139">Crear una cuenta de almacenamiento de Azure mediante el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="e85cb-139">Create an Azure storage account by using hello following code:</span></span>

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. <span data-ttu-id="e85cb-140">Mostrar claves de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e85cb-140">Show hello storage account keys.</span></span>

    <span data-ttu-id="e85cb-141">Cuando se crea una cuenta de almacenamiento, se crean las claves de cuenta de hello en pares para que se pueden girar sin ninguna interrupción del servicio.</span><span class="sxs-lookup"><span data-stu-id="e85cb-141">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="e85cb-142">Cuando cambie toohello segunda clave en el par de hello, cree un nuevo par de claves.</span><span class="sxs-lookup"><span data-stu-id="e85cb-142">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="e85cb-143">Nuevas claves de cuenta de almacenamiento se crean siempre en pares y asegurarse de que siempre tiene al menos un almacenamiento sin usar de tooswitch listo clave a.</span><span class="sxs-lookup"><span data-stu-id="e85cb-143">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage key ready tooswitch to.</span></span> <span data-ttu-id="e85cb-144">claves de cuenta de almacenamiento de hello tooshow, usar hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="e85cb-144">tooshow hello storage account keys, use hello following code:</span></span>

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. <span data-ttu-id="e85cb-145">Crear recurso compartido de almacenamiento de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e85cb-145">Create hello File storage share.</span></span>

    <span data-ttu-id="e85cb-146">recurso compartido de almacenamiento de archivos de Hello contiene el recurso compartido SMB de Hola.</span><span class="sxs-lookup"><span data-stu-id="e85cb-146">hello File storage share contains hello SMB share.</span></span> <span data-ttu-id="e85cb-147">cuota de Hello siempre se expresa en gigabytes (GB).</span><span class="sxs-lookup"><span data-stu-id="e85cb-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="e85cb-148">toocreate Hola recurso compartido de almacenamiento de archivos, usar hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="e85cb-148">toocreate hello File storage share, use hello following code:</span></span>

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. <span data-ttu-id="e85cb-149">Crear el directorio de punto de montaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="e85cb-149">Create hello mount-point directory.</span></span>

    <span data-ttu-id="e85cb-150">Debe crear un directorio local en Hola Hola Linux archivo sistema toomount recurso compartido de SMB.</span><span class="sxs-lookup"><span data-stu-id="e85cb-150">You must create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="e85cb-151">Algo escrito o leer desde el directorio de montaje local Hola se reenvía toohello recurso compartido SMB que se hospeda en el almacenamiento de archivos.</span><span class="sxs-lookup"><span data-stu-id="e85cb-151">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="e85cb-152">directorio de hello toocreate, Hola de uso siguiente código:</span><span class="sxs-lookup"><span data-stu-id="e85cb-152">toocreate hello directory, use hello following code:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. <span data-ttu-id="e85cb-153">Montar Hola recurso compartido SMB mediante el uso de hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="e85cb-153">Mount hello SMB share by using hello following code:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. <span data-ttu-id="e85cb-154">Conservar Hola montar SMB a través de reinicios.</span><span class="sxs-lookup"><span data-stu-id="e85cb-154">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="e85cb-155">Al reiniciar Hola VM de Linux, hello montada de recurso compartido SMB se desmonta durante el cierre.</span><span class="sxs-lookup"><span data-stu-id="e85cb-155">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="e85cb-156">tooremount Hola recurso compartido SMB de arranque, debe agregar una toohello línea Linux/etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="e85cb-156">tooremount hello SMB share on boot, you must add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="e85cb-157">Linux utiliza Hola fstab archivo toolist Hola sistemas de archivos que necesita toomount durante el proceso de arranque de Hola.</span><span class="sxs-lookup"><span data-stu-id="e85cb-157">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="e85cb-158">Agregar recurso compartido SMB Hola garantiza que ese recurso compartido de archivo almacenamiento hello es un sistema de archivos montado permanentemente para hello VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="e85cb-158">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="e85cb-159">Agregar tooa del recurso compartido SMB de hello archivo almacenamiento nueva máquina virtual es posible cuando se usa en la nube init.</span><span class="sxs-lookup"><span data-stu-id="e85cb-159">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="e85cb-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e85cb-160">Next steps</span></span>

- [<span data-ttu-id="e85cb-161">Uso de nube init toocustomize una VM de Linux durante la creación</span><span class="sxs-lookup"><span data-stu-id="e85cb-161">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="e85cb-162">Agregar una VM de Linux tooa de disco</span><span class="sxs-lookup"><span data-stu-id="e85cb-162">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="e85cb-163">Cifrar los discos en una VM Linux mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e85cb-163">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
