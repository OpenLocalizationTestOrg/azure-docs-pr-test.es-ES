---
title: "almacenamiento de archivos de Azure en máquinas virtuales de Linux con SMB aaaMount | Documentos de Microsoft"
description: "¿Cómo toomount almacenamiento de archivos de Azure en máquinas virtuales de Linux con SMB con Hola 2.0 de CLI de Azure"
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
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a><span data-ttu-id="ce335-103">Montaje de Azure File Storage en máquinas virtuales Linux con SMB</span><span class="sxs-lookup"><span data-stu-id="ce335-103">Mount Azure File storage on Linux VMs using SMB</span></span>

<span data-ttu-id="ce335-104">Este artículo muestra cómo montar hello tooutilize servicio de almacenamiento de archivos de Azure en una VM de Linux con SMB con hello 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="ce335-104">This article shows you how tooutilize hello Azure File storage service on a Linux VM using an SMB mount with hello Azure CLI 2.0.</span></span> <span data-ttu-id="ce335-105">Almacenamiento de archivos de Azure ofrece recursos compartidos de archivos en la nube de hello mediante el protocolo SMB estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce335-105">Azure File storage offers file shares in hello cloud using hello standard SMB protocol.</span></span> <span data-ttu-id="ce335-106">También puede realizar estos pasos con hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ce335-106">You can also perform these steps with hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="ce335-107">Hola requisitos son:</span><span class="sxs-lookup"><span data-stu-id="ce335-107">hello requirements are:</span></span>

- <span data-ttu-id="ce335-108">[una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="ce335-108">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
- <span data-ttu-id="ce335-109">[archivos de clave SSH pública y privada](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="ce335-109">[SSH public and private key files](mac-create-ssh-keys.md)</span></span>

## <a name="quick-commands"></a><span data-ttu-id="ce335-110">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="ce335-110">Quick Commands</span></span>

* <span data-ttu-id="ce335-111">Un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="ce335-111">A resource group</span></span>
* <span data-ttu-id="ce335-112">Una red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="ce335-112">An Azure virtual network</span></span>
* <span data-ttu-id="ce335-113">Un grupo de seguridad de red con un SSH entrante</span><span class="sxs-lookup"><span data-stu-id="ce335-113">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="ce335-114">Una subred</span><span class="sxs-lookup"><span data-stu-id="ce335-114">A subnet</span></span>
* <span data-ttu-id="ce335-115">Una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ce335-115">An Azure storage account</span></span>
* <span data-ttu-id="ce335-116">Claves de cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ce335-116">Azure storage account keys</span></span>
* <span data-ttu-id="ce335-117">Un recurso compartido de Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="ce335-117">An Azure File storage share</span></span>
* <span data-ttu-id="ce335-118">Una VM Linux</span><span class="sxs-lookup"><span data-stu-id="ce335-118">A Linux VM</span></span>

<span data-ttu-id="ce335-119">Reemplace los ejemplos por su propia configuración.</span><span class="sxs-lookup"><span data-stu-id="ce335-119">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="ce335-120">Cree un directorio de montaje local Hola</span><span class="sxs-lookup"><span data-stu-id="ce335-120">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="ce335-121">Hola archivo almacenamiento SMB recurso compartido toohello montaje punto de montaje</span><span class="sxs-lookup"><span data-stu-id="ce335-121">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="ce335-122">Conservar el montaje de hello tras un reinicio.</span><span class="sxs-lookup"><span data-stu-id="ce335-122">Persist hello mount after a reboot</span></span>
<span data-ttu-id="ce335-123">toodo por lo tanto, agregar Hola después línea toohello `/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="ce335-123">toodo so, add hello following line toohello `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="ce335-124">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="ce335-124">Detailed walkthrough</span></span>

<span data-ttu-id="ce335-125">Almacenamiento de archivos ofrece recursos compartidos de archivos en la nube de Hola que utilizan el protocolo SMB estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce335-125">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="ce335-126">Con la versión más reciente de Hola de almacenamiento de archivos, también se puede montar un recurso compartido de archivos desde cualquier sistema operativo que admite SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="ce335-126">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="ce335-127">Cuando se usa un montaje SMB en Linux, obtendrá las copias de seguridad fácil tooa robustas y permanente archivado ubicación de almacenamiento que es compatible con un SLA.</span><span class="sxs-lookup"><span data-stu-id="ce335-127">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="ce335-128">Mover archivos de un montaje SMB tooan de máquina virtual que se hospeda en el almacenamiento de archivos es que una excelente manera toodebug registros.</span><span class="sxs-lookup"><span data-stu-id="ce335-128">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="ce335-129">Esto es así porque Hola recurso compartido SMB mismo se puede montar localmente tooyour Mac, Linux o Windows estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ce335-129">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="ce335-130">SMB no es la mejor solución para la transmisión por secuencias Linux de Hola o registros de aplicación en tiempo real, porque Hola protocolo SMB no se generan toohandle tales derechos de registro pesada.</span><span class="sxs-lookup"><span data-stu-id="ce335-130">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="ce335-131">Una herramienta de nivel de registro unificado dedicada como Fluentd sería una opción mejor que SMB para recopilar la salida de registro de la aplicación y Linux.</span><span class="sxs-lookup"><span data-stu-id="ce335-131">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="ce335-132">Para este tutorial detallado, creamos requisitos previos de hello necesario toofirst crear recurso compartido de almacenamiento de archivos de hello y, a continuación, monte a través de SMB en una VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="ce335-132">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="ce335-133">Crear un grupo de recursos con [crear grupo az](/cli/azure/group#create) recurso compartido de archivos de toohold Hola.</span><span class="sxs-lookup"><span data-stu-id="ce335-133">Create a resource group with [az group create](/cli/azure/group#create) toohold hello file share.</span></span>

    <span data-ttu-id="ce335-134">toocreate un grupo de recursos denominado `myResourceGroup` en la ubicación de "West US" Hola, usar hello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ce335-134">toocreate a resource group named `myResourceGroup` in hello "West US" location, use hello following example:</span></span>

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. <span data-ttu-id="ce335-135">Crear una cuenta de almacenamiento de Azure con [crear cuenta de almacenamiento az](/cli/azure/storage/account#create) toostore Hola archivos reales.</span><span class="sxs-lookup"><span data-stu-id="ce335-135">Create an Azure storage account with [az storage account create](/cli/azure/storage/account#create) toostore hello actual files.</span></span>

    <span data-ttu-id="ce335-136">toocreate una cuenta de almacenamiento denominado mystorageaccount mediante hello Standard_LRS almacenamiento SKU, Hola de uso siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ce335-136">toocreate a storage account named mystorageaccount by using hello Standard_LRS storage SKU, use hello following example:</span></span>

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. <span data-ttu-id="ce335-137">Mostrar claves de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce335-137">Show hello storage account keys.</span></span>

    <span data-ttu-id="ce335-138">Cuando se crea una cuenta de almacenamiento, se crean las claves de cuenta de hello en pares para que se pueden girar sin ninguna interrupción del servicio.</span><span class="sxs-lookup"><span data-stu-id="ce335-138">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="ce335-139">Cuando cambie toohello segunda clave en el par de hello, cree un nuevo par de claves.</span><span class="sxs-lookup"><span data-stu-id="ce335-139">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="ce335-140">Nuevas claves de cuenta de almacenamiento se crean siempre en pares, garantizando así que siempre tenga al menos un almacenamiento sin usar cuenta tooswitch clave listo para.</span><span class="sxs-lookup"><span data-stu-id="ce335-140">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage account key ready tooswitch to.</span></span>

    <span data-ttu-id="ce335-141">Ver claves de cuenta de almacenamiento de hello con hello [lista de claves de cuenta de almacenamiento az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="ce335-141">View hello storage account keys with hello [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="ce335-142">Hola claves de cuenta de almacenamiento para hello denominado `mystorageaccount` se muestran en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="ce335-142">hello storage account keys for hello named `mystorageaccount` are listed in hello following example:</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    <span data-ttu-id="ce335-143">tooextract una clave única, utilice hello `--query` marca.</span><span class="sxs-lookup"><span data-stu-id="ce335-143">tooextract a single key, use hello `--query` flag.</span></span> <span data-ttu-id="ce335-144">Hello en el ejemplo siguiente se extrae primera clave de hello (`[0]`):</span><span class="sxs-lookup"><span data-stu-id="ce335-144">hello following example extracts hello first key (`[0]`):</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. <span data-ttu-id="ce335-145">Crear recurso compartido de almacenamiento de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce335-145">Create hello File storage share.</span></span>

    <span data-ttu-id="ce335-146">recurso compartido de almacenamiento de archivos de Hello contiene Hola con recurso compartido SMB [crear recurso compartido de almacenamiento az](/cli/azure/storage/share#create).</span><span class="sxs-lookup"><span data-stu-id="ce335-146">hello File storage share contains hello SMB share with [az storage share create](/cli/azure/storage/share#create).</span></span> <span data-ttu-id="ce335-147">cuota de Hello siempre se expresa en gigabytes (GB).</span><span class="sxs-lookup"><span data-stu-id="ce335-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="ce335-148">Pasar de una de las claves de Hola de hello anterior `az storage account keys list` comando.</span><span class="sxs-lookup"><span data-stu-id="ce335-148">Pass in one of hello keys from hello preceding `az storage account keys list` command.</span></span> <span data-ttu-id="ce335-149">Crear un recurso compartido denominado mystorageshare con una cuota de 10 GB mediante el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="ce335-149">Create a share named mystorageshare with a 10-GB quota by using hello following example:</span></span>

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. <span data-ttu-id="ce335-150">Cree un directorio de punto de montaje.</span><span class="sxs-lookup"><span data-stu-id="ce335-150">Create a mount-point directory.</span></span>

    <span data-ttu-id="ce335-151">Cree un directorio local en Hola Hola Linux archivo sistema toomount recurso compartido de SMB.</span><span class="sxs-lookup"><span data-stu-id="ce335-151">Create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="ce335-152">Algo escrito o leer desde el directorio de montaje local Hola se reenvía toohello recurso compartido SMB que se hospeda en el almacenamiento de archivos.</span><span class="sxs-lookup"><span data-stu-id="ce335-152">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="ce335-153">toocreate un directorio local en/mnt/mymountdirectory, Hola de uso siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ce335-153">toocreate a local directory at /mnt/mymountdirectory, use hello following example:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. <span data-ttu-id="ce335-154">Montar el directorio local del toohello de recurso compartido SMB Hola.</span><span class="sxs-lookup"><span data-stu-id="ce335-154">Mount hello SMB share toohello local directory.</span></span>

    <span data-ttu-id="ce335-155">Proporcionar su propio nombre de usuario de cuenta de almacenamiento y la clave de cuenta de almacenamiento para las credenciales de montaje de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="ce335-155">Provide your own storage account username and storage account key for hello mount credentials as follows:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. <span data-ttu-id="ce335-156">Conservar Hola montar SMB a través de reinicios.</span><span class="sxs-lookup"><span data-stu-id="ce335-156">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="ce335-157">Al reiniciar Hola VM de Linux, hello montada de recurso compartido SMB se desmonta durante el cierre.</span><span class="sxs-lookup"><span data-stu-id="ce335-157">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="ce335-158">Hola tooremount recurso compartido SMB en el arranque, agregar un toohello línea Linux/etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="ce335-158">tooremount hello SMB share on boot, add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="ce335-159">Linux utiliza Hola fstab archivo toolist Hola sistemas de archivos que necesita toomount durante el proceso de arranque de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce335-159">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="ce335-160">Agregar recurso compartido SMB Hola garantiza que ese recurso compartido de archivo almacenamiento hello es un sistema de archivos montado permanentemente para hello VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="ce335-160">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="ce335-161">Agregar tooa del recurso compartido SMB de hello archivo almacenamiento nueva máquina virtual es posible cuando se usa en la nube init.</span><span class="sxs-lookup"><span data-stu-id="ce335-161">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="ce335-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ce335-162">Next steps</span></span>

- [<span data-ttu-id="ce335-163">Uso de nube init toocustomize una VM de Linux durante la creación</span><span class="sxs-lookup"><span data-stu-id="ce335-163">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="ce335-164">Agregar una VM de Linux tooa de disco</span><span class="sxs-lookup"><span data-stu-id="ce335-164">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="ce335-165">Cifrar los discos en una VM Linux mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="ce335-165">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
