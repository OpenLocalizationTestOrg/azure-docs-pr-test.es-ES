---
title: Uso de Azure File Storage con Linux | Microsoft Docs
description: Aprenda a montar un recurso compartido de archivos de Azure mediante SMB en Linux.
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6edc37ce-698f-4d50-8fc1-591ad456175d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/8/2017
ms.author: renash
ms.openlocfilehash: 27b393a899c60a3a0393619f338a396dff659498
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="b8465-103">Uso de Azure File Storage con Linux</span><span class="sxs-lookup"><span data-stu-id="b8465-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="b8465-104">[Azure File Storage](storage-dotnet-how-to-use-files.md) es el sistema de archivos en la nube de Microsoft fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="b8465-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="b8465-105">Los recursos compartidos de Azure File se pueden montar en distribuciones de Linux mediante el [paquete cifs-utils](https://wiki.samba.org/index.php/LinuxCIFS_utils) del [proyecto de Samba](https://www.samba.org/).</span><span class="sxs-lookup"><span data-stu-id="b8465-105">Azure File shares can be mounted in Linux distributions using the [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from the [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="b8465-106">En este artículo se muestran dos maneras de montar un recurso compartido de Azure File: a petición, con el comando `mount` y al inicio, mediante la creación de una entrada en `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="b8465-106">This article shows two ways to mount an Azure File share: on-demand with the `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="b8465-107">Para montar un recurso compartido de Azure File fuera de la región de Azure en la que se hospeda, bien sea en local o en una región distinta de Azure, el sistema operativo debe admitir la funcionalidad de cifrado de SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="b8465-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support the encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="b8465-108">La característica de cifrado de SMB 3.0 para Linux se introdujo en el kernel 4.11.</span><span class="sxs-lookup"><span data-stu-id="b8465-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="b8465-109">Esta característica permite el montaje de recursos compartidos de Azure File desde el entorno local o una región distinta de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8465-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="b8465-110">En el momento de la publicación, esta funcionalidad se ha usado en Ubuntu 16.04 y en versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="b8465-110">At the time of publishing, this functionality has been backported to Ubuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-the-cifs-utils-package"></a><span data-ttu-id="b8465-111">Requisitos previos para el montaje de un recurso compartido de Azure File con Linux y el paquete cifs-utils</span><span class="sxs-lookup"><span data-stu-id="b8465-111">Prerequisities for mounting an Azure File share with Linux and the cifs-utils package</span></span>
* <span data-ttu-id="b8465-112">**Seleccionar una distribución de Linux que pueda tener instalado el paquete cifs-utils**: Microsoft recomienda las siguientes distribuciones de Linux de la galería de imágenes de Azure:</span><span class="sxs-lookup"><span data-stu-id="b8465-112">**Pick a Linux distribution that can have the cifs-utils package installed**: Microsoft recommends the following Linux distributions in the Azure image gallery:</span></span>

    * <span data-ttu-id="b8465-113">Ubuntu Server 14.04+</span><span class="sxs-lookup"><span data-stu-id="b8465-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="b8465-114">RHEL 7+</span><span class="sxs-lookup"><span data-stu-id="b8465-114">RHEL 7+</span></span>
    * <span data-ttu-id="b8465-115">CentOS 7+</span><span class="sxs-lookup"><span data-stu-id="b8465-115">CentOS 7+</span></span>
    * <span data-ttu-id="b8465-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="b8465-116">Debian 8</span></span>
    * <span data-ttu-id="b8465-117">openSUSE 13.2+</span><span class="sxs-lookup"><span data-stu-id="b8465-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="b8465-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="b8465-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="b8465-119"><a id="install-cifs-utils"></a>**El paquete cifs-utils está instalado**: este paquete se puede instalar con el administrador de paquetes de la distribución de Linux de su elección.</span><span class="sxs-lookup"><span data-stu-id="b8465-119"><a id="install-cifs-utils"></a>**The cifs-utils package is installed**: The cifs-utils can be installed using the package manager on the Linux distribution of your choice.</span></span> 

    <span data-ttu-id="b8465-120">En distribuciones de **Ubuntu** y **Debian**, use el administrador de paquetes `apt-get`:</span><span class="sxs-lookup"><span data-stu-id="b8465-120">On **Ubuntu** and **Debian-based** distributions, use the `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="b8465-121">En **RHEL** y **CentOS**, use el administrador de paquetes `yum`:</span><span class="sxs-lookup"><span data-stu-id="b8465-121">On **RHEL** and **CentOS**, use the `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="b8465-122">En **openSUSE**, use el administrador de paquetes `zypper`:</span><span class="sxs-lookup"><span data-stu-id="b8465-122">On **openSUSE**, use the `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="b8465-123">En otras distribuciones, use el administrador de paquetes apropiado o [compile desde el origen](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="b8465-123">On other distributions, use the appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="b8465-124">**Decidir sobre los permisos de archivo o directorio del recurso compartido montado**: en los ejemplos siguientes, usamos 0777 para proporcionar permisos de lectura, escritura y ejecución a todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="b8465-124">**Decide on the directory/file permissions of the mounted share**: In the examples below, we use 0777, to give read, write, and execute permissions to all users.</span></span> <span data-ttu-id="b8465-125">Puede reemplazarlos por otros [permisos chmod](https://en.wikipedia.org/wiki/Chmod), según prefiera.</span><span class="sxs-lookup"><span data-stu-id="b8465-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="b8465-126">**Nombre de la cuenta de almacenamiento**: para montar un recurso compartido de archivos de Azure, necesitará el nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b8465-126">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="b8465-127">**Clave de la cuenta de almacenamiento**: para montar un recurso compartido de archivos de Azure, necesitará la clave principal (o secundaria) de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b8465-127">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="b8465-128">Actualmente no se admiten claves SAS para el montaje.</span><span class="sxs-lookup"><span data-stu-id="b8465-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="b8465-129">**Asegurarse de que el puerto 445 está abierto**: SMB se comunica a través del puerto TCP 445, así que compruebe que el firewall no bloquea el puerto TCP 445 en la máquina cliente.</span><span class="sxs-lookup"><span data-stu-id="b8465-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="b8465-130">Montaje del recurso compartido de Azure File a petición con `mount`</span><span class="sxs-lookup"><span data-stu-id="b8465-130">Mount the Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="b8465-131">**[Instale el paquete cifs-utils correspondiente a su distribución de Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="b8465-131">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="b8465-132">**Cree una carpeta para el punto de montaje**: esta operación se puede hacer en cualquier parte del sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="b8465-132">**Create a folder for the mount point**: This can be done anywhere on the file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="b8465-133">**Use el comando mount para montar el recurso compartido de Azure File**: no olvide reemplazar `<storage-account-name>`, `<share-name>`, `<storage-account-key>` y por la información correcta.</span><span class="sxs-lookup"><span data-stu-id="b8465-133">**Use the mount command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="b8465-134">Cuando haya terminado de usar el recurso compartido de Azure File, puede usar `sudo umount ./mymountpoint` para desmontarlo.</span><span class="sxs-lookup"><span data-stu-id="b8465-134">When you are done using the Azure File share, you may use `sudo umount ./mymountpoint` to unmount the share.</span></span>

## <a name="create-a-persistent-mount-point-for-the-azure-file-share-with-etcfstab"></a><span data-ttu-id="b8465-135">Creación de un punto de montaje persistente para el recurso compartido de Azure File`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="b8465-135">Create a persistent mount point for the Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="b8465-136">**[Instale el paquete cifs-utils correspondiente a su distribución de Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="b8465-136">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="b8465-137">**Cree una carpeta para el punto de montaje**: esta operación se puede realizar en cualquier parte del sistema de archivos, pero debe tener en cuenta la ruta de acceso absoluta de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="b8465-137">**Create a folder for the mount point**: This can be done anywhere on the file system, but you need to note the absolute path of the folder.</span></span> <span data-ttu-id="b8465-138">En el ejemplo siguiente se crea una carpeta en la raíz.</span><span class="sxs-lookup"><span data-stu-id="b8465-138">The following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="b8465-139">**Use el siguiente comando para anexar la siguiente línea a `/etc/fstab`** : no olvide reemplazar `<storage-account-name>`, `<share-name>`, y `<storage-account-key>` por la información correcta.</span><span class="sxs-lookup"><span data-stu-id="b8465-139">**Use the following command to append the following line to `/etc/fstab`**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="b8465-140">Puede usar `sudo mount -a` para montar el recurso compartido de Azure File después de editar `/etc/fstab` en lugar de reiniciar el sistema.</span><span class="sxs-lookup"><span data-stu-id="b8465-140">You can use `sudo mount -a` to mount the Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="b8465-141">Comentarios</span><span class="sxs-lookup"><span data-stu-id="b8465-141">Feedback</span></span>
<span data-ttu-id="b8465-142">Usuarios de Linux: nos gustaría conocer su opinión.</span><span class="sxs-lookup"><span data-stu-id="b8465-142">Linux users, we want to hear from you!</span></span>

<span data-ttu-id="b8465-143">Azure File Storage para el grupo de usuarios de Linux cuenta con un foro donde puede compartir sus comentarios a medida que evalúa y adopta File Storage en Linux.</span><span class="sxs-lookup"><span data-stu-id="b8465-143">The Azure File storage for Linux users' group provides a forum for you to share feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="b8465-144">Envíe un correo electrónico a [Usuarios de Linux de Azure File Storage](mailto:azurefileslinuxusers@microsoft.com) para unirse al grupo de usuarios.</span><span class="sxs-lookup"><span data-stu-id="b8465-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) to join the users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8465-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b8465-145">Next steps</span></span>
<span data-ttu-id="b8465-146">Consulte los vínculos siguientes para obtener más información acerca Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="b8465-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="b8465-147">Referencia de la API REST del servicio de archivos</span><span class="sxs-lookup"><span data-stu-id="b8465-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="b8465-148">Usar Azure PowerShell con Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b8465-148">Using Azure PowerShell with Azure storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="b8465-149">Uso de AzCopy con Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b8465-149">How to use AzCopy with Microsoft Azure storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="b8465-150">Uso de la CLI de Azure con Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b8465-150">Using the Azure CLI with Azure storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="b8465-151">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="b8465-151">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="b8465-152">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="b8465-152">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)
