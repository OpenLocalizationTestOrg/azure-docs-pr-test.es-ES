---
title: almacenamiento de archivos de Azure con Linux aaaUse | Documentos de Microsoft
description: "Obtenga información acerca de cómo compartir toomount un archivo de Azure a través de SMB en Linux."
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
ms.openlocfilehash: eeaa24b7f9e646724c5d86ae1e80dfdadaff34fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="f37f9-103">Uso de Azure File Storage con Linux</span><span class="sxs-lookup"><span data-stu-id="f37f9-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="f37f9-104">[Almacenamiento de Azure archivo](../storage-dotnet-how-to-use-files.md) es sistema de archivos de nube de Microsoft toouse fácil.</span><span class="sxs-lookup"><span data-stu-id="f37f9-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="f37f9-105">Azure recursos compartidos de archivos se pueden montar en las distribuciones de Linux con hello [cifs-utils paquete](https://wiki.samba.org/index.php/LinuxCIFS_utils) de hello [proyecto Samba](https://www.samba.org/).</span><span class="sxs-lookup"><span data-stu-id="f37f9-105">Azure File shares can be mounted in Linux distributions using hello [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from hello [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="f37f9-106">Este artículo muestra un recurso compartido de archivos de Azure de toomount de dos maneras: a petición con hello `mount` de comandos y de arranque mediante la creación de una entrada en `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="f37f9-106">This article shows two ways toomount an Azure File share: on-demand with hello `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="f37f9-107">En orden toomount un recurso compartido de archivos de Azure fuera Hola región de Azure que se hospeda en, como local o en una región distinta de Azure, Hola SO debe admitir funcionalidad de cifrado de Hola de SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="f37f9-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support hello encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="f37f9-108">La característica de cifrado de SMB 3.0 para Linux se introdujo en el kernel 4.11.</span><span class="sxs-lookup"><span data-stu-id="f37f9-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="f37f9-109">Esta característica permite el montaje de recursos compartidos de Azure File desde el entorno local o una región distinta de Azure.</span><span class="sxs-lookup"><span data-stu-id="f37f9-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="f37f9-110">En tiempo de presentación de la publicación, esta funcionalidad ha sido utilizados tooUbuntu desde 16.04 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="f37f9-110">At hello time of publishing, this functionality has been backported tooUbuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a><span data-ttu-id="f37f9-111">Requisitos previos para el montaje de un recurso compartido de archivos de Azure paquete cifs-utils hello y Linux</span><span class="sxs-lookup"><span data-stu-id="f37f9-111">Prerequisities for mounting an Azure File share with Linux and hello cifs-utils package</span></span>
* <span data-ttu-id="f37f9-112">**Seleccionar una distribución de Linux que se puede tener instalado el paquete de utilidades de cifs Hola**: Microsoft recomienda Hola siguiendo las distribuciones de Linux en la Galería de imágenes de Azure hello:</span><span class="sxs-lookup"><span data-stu-id="f37f9-112">**Pick a Linux distribution that can have hello cifs-utils package installed**: Microsoft recommends hello following Linux distributions in hello Azure image gallery:</span></span>

    * <span data-ttu-id="f37f9-113">Ubuntu Server 14.04+</span><span class="sxs-lookup"><span data-stu-id="f37f9-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="f37f9-114">RHEL 7+</span><span class="sxs-lookup"><span data-stu-id="f37f9-114">RHEL 7+</span></span>
    * <span data-ttu-id="f37f9-115">CentOS 7+</span><span class="sxs-lookup"><span data-stu-id="f37f9-115">CentOS 7+</span></span>
    * <span data-ttu-id="f37f9-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="f37f9-116">Debian 8</span></span>
    * <span data-ttu-id="f37f9-117">openSUSE 13.2+</span><span class="sxs-lookup"><span data-stu-id="f37f9-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="f37f9-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="f37f9-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="f37f9-119"><a id="install-cifs-utils"></a>**Hello cifs-utils paquete está instalado**: Hola cifs-utils puede instalarse mediante el Administrador de paquetes de saludo en la distribución de Linux Hola de su elección.</span><span class="sxs-lookup"><span data-stu-id="f37f9-119"><a id="install-cifs-utils"></a>**hello cifs-utils package is installed**: hello cifs-utils can be installed using hello package manager on hello Linux distribution of your choice.</span></span> 

    <span data-ttu-id="f37f9-120">En **Ubuntu** y **Debian-based** distribuciones, usar hello `apt-get` Administrador de paquetes:</span><span class="sxs-lookup"><span data-stu-id="f37f9-120">On **Ubuntu** and **Debian-based** distributions, use hello `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="f37f9-121">En **RHEL** y **CentOS**, usar hello `yum` Administrador de paquetes:</span><span class="sxs-lookup"><span data-stu-id="f37f9-121">On **RHEL** and **CentOS**, use hello `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="f37f9-122">En **openSUSE**, usar hello `zypper` Administrador de paquetes:</span><span class="sxs-lookup"><span data-stu-id="f37f9-122">On **openSUSE**, use hello `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="f37f9-123">En otras distribuciones, utilice el Administrador de paquetes apropiada de Hola o [compilar desde origen](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="f37f9-123">On other distributions, use hello appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="f37f9-124">**Decidir de permisos de directorios/archivos de hello del recurso compartido montado de Hola**: en los siguientes ejemplos de hello, usamos 0777, toogive leer, escribir y ejecutar los usuarios de tooall de permisos.</span><span class="sxs-lookup"><span data-stu-id="f37f9-124">**Decide on hello directory/file permissions of hello mounted share**: In hello examples below, we use 0777, toogive read, write, and execute permissions tooall users.</span></span> <span data-ttu-id="f37f9-125">Puede reemplazarlos por otros [permisos chmod](https://en.wikipedia.org/wiki/Chmod), según prefiera.</span><span class="sxs-lookup"><span data-stu-id="f37f9-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="f37f9-126">**Nombre de la cuenta de almacenamiento**: toomount compartir de un archivo de Azure, se necesita Hola nombre de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="f37f9-126">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="f37f9-127">**Clave de la cuenta de almacenamiento**: toomount compartir de un archivo de Azure, se necesita Hola clave de almacenamiento principal (o secundario).</span><span class="sxs-lookup"><span data-stu-id="f37f9-127">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="f37f9-128">Actualmente no se admiten claves SAS para el montaje.</span><span class="sxs-lookup"><span data-stu-id="f37f9-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="f37f9-129">**Asegúrese de que el puerto 445 está abierto**: SMB se comunica a través del puerto TCP 445 - comprobar toosee si el firewall no bloquea el TCP puertos 445 del equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="f37f9-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="f37f9-130">Montar Hola a petición con recurso compartido de archivos de Azure`mount`</span><span class="sxs-lookup"><span data-stu-id="f37f9-130">Mount hello Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="f37f9-131">**[Instalar el paquete de utilidades de cifs Hola para su distribución de Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="f37f9-131">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="f37f9-132">**Cree una carpeta para el punto de montaje de Hola**: Esto puede realizarse en cualquier lugar en el sistema de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f37f9-132">**Create a folder for hello mount point**: This can be done anywhere on hello file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="f37f9-133">**Use Hola montaje comando toomount hello Azure recurso compartido de archivos**: Recuerde tooreplace `<storage-account-name>`, `<share-name>`, y `<storage-account-key>` con la información adecuada Hola.</span><span class="sxs-lookup"><span data-stu-id="f37f9-133">**Use hello mount command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="f37f9-134">Cuando haya terminado de usar Hola recurso compartido de archivos de Azure, puede usar `sudo umount ./mymountpoint` recurso compartido de hello toounmount.</span><span class="sxs-lookup"><span data-stu-id="f37f9-134">When you are done using hello Azure File share, you may use `sudo umount ./mymountpoint` toounmount hello share.</span></span>

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a><span data-ttu-id="f37f9-135">Crear un punto de montaje persistente para hello Azure recurso compartido de archivos`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="f37f9-135">Create a persistent mount point for hello Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="f37f9-136">**[Instalar el paquete de utilidades de cifs Hola para su distribución de Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="f37f9-136">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="f37f9-137">**Cree una carpeta para el punto de montaje de Hola**: Esto puede realizarse en cualquier lugar en el sistema de archivos de hello, pero debe toonote Hola ruta de acceso absoluta carpeta Hola.</span><span class="sxs-lookup"><span data-stu-id="f37f9-137">**Create a folder for hello mount point**: This can be done anywhere on hello file system, but you need toonote hello absolute path of hello folder.</span></span> <span data-ttu-id="f37f9-138">Hola de ejemplo siguiente crea una carpeta bajo la raíz.</span><span class="sxs-lookup"><span data-stu-id="f37f9-138">hello following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="f37f9-139">**Siguiente Hola de uso de comandos hello tooappend siguen demasiado`/etc/fstab`**: Recuerde tooreplace `<storage-account-name>`, `<share-name>`, y `<storage-account-key>` con la información adecuada Hola.</span><span class="sxs-lookup"><span data-stu-id="f37f9-139">**Use hello following command tooappend hello following line too`/etc/fstab`**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="f37f9-140">Puede usar `sudo mount -a` toomount recurso compartido de archivos de Azure de hello después de editar `/etc/fstab` en lugar de reiniciar el sistema.</span><span class="sxs-lookup"><span data-stu-id="f37f9-140">You can use `sudo mount -a` toomount hello Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="f37f9-141">Comentarios</span><span class="sxs-lookup"><span data-stu-id="f37f9-141">Feedback</span></span>
<span data-ttu-id="f37f9-142">Los usuarios de Linux, dudes toohear del usuario.</span><span class="sxs-lookup"><span data-stu-id="f37f9-142">Linux users, we want toohear from you!</span></span>

<span data-ttu-id="f37f9-143">Hola almacenamiento de archivos de Azure para el grupo de usuarios de Linux proporciona un foro para usted tooshare comentarios como evaluar y adoptar el almacenamiento de archivos en Linux.</span><span class="sxs-lookup"><span data-stu-id="f37f9-143">hello Azure File storage for Linux users' group provides a forum for you tooshare feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="f37f9-144">Correo electrónico [almacenamiento de archivos de Azure a los usuarios de Linux](mailto:azurefileslinuxusers@microsoft.com) grupo de usuarios de toojoin Hola.</span><span class="sxs-lookup"><span data-stu-id="f37f9-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) toojoin hello users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f37f9-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f37f9-145">Next steps</span></span>
<span data-ttu-id="f37f9-146">Consulte los vínculos siguientes para obtener más información acerca Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="f37f9-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="f37f9-147">Referencia de la API REST del servicio de archivos</span><span class="sxs-lookup"><span data-stu-id="f37f9-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="f37f9-148">Cómo toouse AzCopy con almacenamiento de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f37f9-148">How toouse AzCopy with Microsoft Azure storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="f37f9-149">Uso de hello CLI de Azure con el almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="f37f9-149">Using hello Azure CLI with Azure storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="f37f9-150">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="f37f9-150">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="f37f9-151">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="f37f9-151">Troubleshooting</span></span>](storage-troubleshoot-linux-file-connection-problems.md)
