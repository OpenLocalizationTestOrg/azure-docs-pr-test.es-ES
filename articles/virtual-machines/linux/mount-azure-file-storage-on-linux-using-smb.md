---
title: "Montaje de Azure File Storage en máquinas virtuales Linux con SMB | Microsoft Docs"
description: "Procedimientos de montaje de Azure File Storage en máquinas virtuales Linux mediante SMB con la CLI de Azure 2.0"
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
ms.openlocfilehash: 9eae17b304f8a987b44ebed8906dabd8ff3a36a8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a><span data-ttu-id="eec76-103">Montaje de Azure File Storage en máquinas virtuales Linux con SMB</span><span class="sxs-lookup"><span data-stu-id="eec76-103">Mount Azure File storage on Linux VMs using SMB</span></span>

<span data-ttu-id="eec76-104">En este artículo se muestra cómo usar el servicio Azure File Storage en una máquina virtual Linux mediante un montaje de SMB con la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="eec76-104">This article shows you how to utilize the Azure File storage service on a Linux VM using an SMB mount with the Azure CLI 2.0.</span></span> <span data-ttu-id="eec76-105">El almacenamiento de archivos de Azure ofrece recursos compartidos de archivos en la nube mediante el protocolo SMB estándar.</span><span class="sxs-lookup"><span data-stu-id="eec76-105">Azure File storage offers file shares in the cloud using the standard SMB protocol.</span></span> <span data-ttu-id="eec76-106">También puede llevar a cabo estos pasos con la [CLI de Azure 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eec76-106">You can also perform these steps with the [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="eec76-107">Los requisitos son:</span><span class="sxs-lookup"><span data-stu-id="eec76-107">The requirements are:</span></span>

- <span data-ttu-id="eec76-108">[una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="eec76-108">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
- <span data-ttu-id="eec76-109">[archivos de clave SSH pública y privada](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="eec76-109">[SSH public and private key files](mac-create-ssh-keys.md)</span></span>

## <a name="quick-commands"></a><span data-ttu-id="eec76-110">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="eec76-110">Quick Commands</span></span>

* <span data-ttu-id="eec76-111">Un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="eec76-111">A resource group</span></span>
* <span data-ttu-id="eec76-112">Una red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="eec76-112">An Azure virtual network</span></span>
* <span data-ttu-id="eec76-113">Un grupo de seguridad de red con un SSH entrante</span><span class="sxs-lookup"><span data-stu-id="eec76-113">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="eec76-114">Una subred</span><span class="sxs-lookup"><span data-stu-id="eec76-114">A subnet</span></span>
* <span data-ttu-id="eec76-115">Una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="eec76-115">An Azure storage account</span></span>
* <span data-ttu-id="eec76-116">Claves de cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="eec76-116">Azure storage account keys</span></span>
* <span data-ttu-id="eec76-117">Un recurso compartido de Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="eec76-117">An Azure File storage share</span></span>
* <span data-ttu-id="eec76-118">Una VM Linux</span><span class="sxs-lookup"><span data-stu-id="eec76-118">A Linux VM</span></span>

<span data-ttu-id="eec76-119">Reemplace los ejemplos por su propia configuración.</span><span class="sxs-lookup"><span data-stu-id="eec76-119">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-the-local-mount"></a><span data-ttu-id="eec76-120">Creación de un directorio para el montaje local</span><span class="sxs-lookup"><span data-stu-id="eec76-120">Create a directory for the local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-the-file-storage-smb-share-to-the-mount-point"></a><span data-ttu-id="eec76-121">Montaje del recurso compartido de SMB de File Storage en el punto de montaje</span><span class="sxs-lookup"><span data-stu-id="eec76-121">Mount the File storage SMB share to the mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-the-mount-after-a-reboot"></a><span data-ttu-id="eec76-122">Conserve el montaje tras un reinicio</span><span class="sxs-lookup"><span data-stu-id="eec76-122">Persist the mount after a reboot</span></span>
<span data-ttu-id="eec76-123">Para ello, agregue la siguiente línea a `/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="eec76-123">To do so, add the following line to the `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="eec76-124">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="eec76-124">Detailed walkthrough</span></span>

<span data-ttu-id="eec76-125">El almacenamiento de archivos ofrece recursos compartidos de archivos en la nube que usan el protocolo SMB estándar.</span><span class="sxs-lookup"><span data-stu-id="eec76-125">File storage offers file shares in the cloud that use the standard SMB protocol.</span></span> <span data-ttu-id="eec76-126">Con la versión más reciente de File Storage, también es posible montar un recurso compartido de archivos desde cualquier SO que sea compatible con SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="eec76-126">With the latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="eec76-127">Cuando se usa un montaje de SMB en Linux se obtienen copias de seguridad fáciles en una ubicación de almacenamiento de archivado permanente y sólida que se proporciona mediante un Acuerdo de Nivel de Servicio.</span><span class="sxs-lookup"><span data-stu-id="eec76-127">When you use an SMB mount on Linux, you get easy backups to a robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="eec76-128">El movimiento de archivos de una VM a un montaje de SMB que se hospeda en File Storage es una excelente manera de depurar registros.</span><span class="sxs-lookup"><span data-stu-id="eec76-128">Moving files from a VM to an SMB mount that's hosted on File storage is a great way to debug logs.</span></span> <span data-ttu-id="eec76-129">Eso es porque se puede montar el mismo recurso compartido SMB localmente en la estación de trabajo de Windows, Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="eec76-129">That's because the same SMB share can be mounted locally to your Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="eec76-130">SMB no es la mejor solución para transmitir registros de aplicación o Linux en tiempo real porque el protocolo SMB no está creado para controlar tareas de registro tan pesadas.</span><span class="sxs-lookup"><span data-stu-id="eec76-130">SMB isn't the best solution for streaming Linux or application logs in real time, because the SMB protocol is not built to handle such heavy logging duties.</span></span> <span data-ttu-id="eec76-131">Una herramienta de nivel de registro unificado dedicada como Fluentd sería una opción mejor que SMB para recopilar la salida de registro de la aplicación y Linux.</span><span class="sxs-lookup"><span data-stu-id="eec76-131">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="eec76-132">Para este tutorial detallado, desarrollamos los requisitos previos necesarios para crear primero el recurso compartido de File Storage y luego montarlo a través de SMB en una VM Linux.</span><span class="sxs-lookup"><span data-stu-id="eec76-132">For this detailed walkthrough, we create the prerequisites needed to first create the File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="eec76-133">Cree un grupo de recursos con [az group create](/cli/azure/group#create) para que contenga el recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="eec76-133">Create a resource group with [az group create](/cli/azure/group#create) to hold the file share.</span></span>

    <span data-ttu-id="eec76-134">Para crear un grupo de recursos llamado `myResourceGroup` en la ubicación "Oeste de EE. UU.", use el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="eec76-134">To create a resource group named `myResourceGroup` in the "West US" location, use the following example:</span></span>

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. <span data-ttu-id="eec76-135">Cree una cuenta de almacenamiento de Azure con [az storage account create](/cli/azure/storage/account#create) para almacenar los archivos reales.</span><span class="sxs-lookup"><span data-stu-id="eec76-135">Create an Azure storage account with [az storage account create](/cli/azure/storage/account#create) to store the actual files.</span></span>

    <span data-ttu-id="eec76-136">Para crear una cuenta de almacenamiento llamada mystorageaccount mediante la SKU de almacenamiento Standard_LRS, use el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="eec76-136">To create a storage account named mystorageaccount by using the Standard_LRS storage SKU, use the following example:</span></span>

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. <span data-ttu-id="eec76-137">Muestre las claves de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="eec76-137">Show the storage account keys.</span></span>

    <span data-ttu-id="eec76-138">Cuando cree una cuenta de almacenamiento, las claves de cuenta de almacenamiento se crean en pares de modo que las claves se pueden girar sin ninguna interrupción del servicio.</span><span class="sxs-lookup"><span data-stu-id="eec76-138">When you create a storage account, the account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="eec76-139">Cuando cambia a la segunda clave del par, se crea un nuevo par de claves.</span><span class="sxs-lookup"><span data-stu-id="eec76-139">When you switch to the second key in the pair, you create a new key pair.</span></span> <span data-ttu-id="eec76-140">Las nuevas claves de la cuenta de almacenamiento se crean siempre por pares, lo que garantiza que siempre tenga al menos una clave de cuenta de almacenamiento sin usar lista para cambiar.</span><span class="sxs-lookup"><span data-stu-id="eec76-140">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage account key ready to switch to.</span></span>

    <span data-ttu-id="eec76-141">Vea las claves de la cuenta de almacenamiento con [az storage account keys list](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="eec76-141">View the storage account keys with the [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="eec76-142">Las claves de la cuenta de almacenamiento de la denominada `mystorageaccount` se muestran en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="eec76-142">The storage account keys for the named `mystorageaccount` are listed in the following example:</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    <span data-ttu-id="eec76-143">Para extraer una sola clave, use la marca `--query`.</span><span class="sxs-lookup"><span data-stu-id="eec76-143">To extract a single key, use the `--query` flag.</span></span> <span data-ttu-id="eec76-144">En el ejemplo siguiente se extrae la primera clave (`[0]`):</span><span class="sxs-lookup"><span data-stu-id="eec76-144">The following example extracts the first key (`[0]`):</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. <span data-ttu-id="eec76-145">Cree el recurso compartido de File Storage.</span><span class="sxs-lookup"><span data-stu-id="eec76-145">Create the File storage share.</span></span>

    <span data-ttu-id="eec76-146">El recurso compartido de File Storage contiene el recurso compartido de SMB con [az storage share create](/cli/azure/storage/share#create).</span><span class="sxs-lookup"><span data-stu-id="eec76-146">The File storage share contains the SMB share with [az storage share create](/cli/azure/storage/share#create).</span></span> <span data-ttu-id="eec76-147">La cuota siempre se expresa en gigabytes (GB).</span><span class="sxs-lookup"><span data-stu-id="eec76-147">The quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="eec76-148">Pase una de las claves desde el comando `az storage account keys list` anterior.</span><span class="sxs-lookup"><span data-stu-id="eec76-148">Pass in one of the keys from the preceding `az storage account keys list` command.</span></span> <span data-ttu-id="eec76-149">Cree un recurso compartido llamado mystorageshare con una cuota de 10 GB mediante el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="eec76-149">Create a share named mystorageshare with a 10-GB quota by using the following example:</span></span>

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. <span data-ttu-id="eec76-150">Cree un directorio de punto de montaje.</span><span class="sxs-lookup"><span data-stu-id="eec76-150">Create a mount-point directory.</span></span>

    <span data-ttu-id="eec76-151">Cree un directorio local en el sistema de archivos de Linux en el que montar el recurso compartido de SMB.</span><span class="sxs-lookup"><span data-stu-id="eec76-151">Create a local directory in the Linux file system to mount the SMB share to.</span></span> <span data-ttu-id="eec76-152">No se envía nada escrito o leído desde el directorio de montaje local al recurso compartido de SMB hospedado en File Storage.</span><span class="sxs-lookup"><span data-stu-id="eec76-152">Anything written or read from the local mount directory is forwarded to the SMB share that's hosted on File storage.</span></span> <span data-ttu-id="eec76-153">Para crear un directorio local en /mnt/mymountdirectory, use el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="eec76-153">To create a local directory at /mnt/mymountdirectory, use the following example:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. <span data-ttu-id="eec76-154">Monte el recurso compartido de SMB en el directorio local.</span><span class="sxs-lookup"><span data-stu-id="eec76-154">Mount the SMB share to the local directory.</span></span>

    <span data-ttu-id="eec76-155">Indique el nombre de usuario y la clave de su cuenta de almacenamiento en las credenciales de montaje de esta forma:</span><span class="sxs-lookup"><span data-stu-id="eec76-155">Provide your own storage account username and storage account key for the mount credentials as follows:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. <span data-ttu-id="eec76-156">Conserve el montaje de SMB a través de reinicios.</span><span class="sxs-lookup"><span data-stu-id="eec76-156">Persist the SMB mount through reboots.</span></span>

    <span data-ttu-id="eec76-157">Cuando reinicie la VM de Linux, el recurso compartido de SMB montado se desmontará durante el cierre.</span><span class="sxs-lookup"><span data-stu-id="eec76-157">When you reboot the Linux VM, the mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="eec76-158">Para volver a montar el recurso compartido de SMB al inicio, agregue una línea a /etc/fstab de Linux.</span><span class="sxs-lookup"><span data-stu-id="eec76-158">To remount the SMB share on boot, add a line to the Linux /etc/fstab.</span></span> <span data-ttu-id="eec76-159">Linux utiliza el archivo fstab para enumerar los sistemas de archivos que necesita montar durante el proceso de arranque.</span><span class="sxs-lookup"><span data-stu-id="eec76-159">Linux uses the fstab file to list the file systems that it needs to mount during the boot process.</span></span> <span data-ttu-id="eec76-160">Agregue el recurso compartido de SMB para garantizar que el recurso compartido de File Storage es un sistema de archivos montado de manera permanente para la VM Linux.</span><span class="sxs-lookup"><span data-stu-id="eec76-160">Adding the SMB share ensures that the File storage share is a permanently mounted file system for the Linux VM.</span></span> <span data-ttu-id="eec76-161">La adición del recurso compartido de SMB de File Storage a una nueva VM es posible cuando se usa cloud-init.</span><span class="sxs-lookup"><span data-stu-id="eec76-161">Adding the File storage SMB share to a new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="eec76-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eec76-162">Next steps</span></span>

- [<span data-ttu-id="eec76-163">Uso de cloud-init para personalizar una VM de Linux durante la creación</span><span class="sxs-lookup"><span data-stu-id="eec76-163">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="eec76-164">Adición de un disco a una máquina virtual de Linux</span><span class="sxs-lookup"><span data-stu-id="eec76-164">Add a disk to a Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="eec76-165">Cifrado de discos en una VM Linux mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="eec76-165">Encrypt disks on a Linux VM by using the Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
