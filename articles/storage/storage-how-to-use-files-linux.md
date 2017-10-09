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
ms.openlocfilehash: ed6ba9b98f121d6629d858320ca3760384303ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a>Uso de Azure File Storage con Linux
[Almacenamiento de Azure archivo](storage-dotnet-how-to-use-files.md) es sistema de archivos de nube de Microsoft toouse fácil. Azure recursos compartidos de archivos se pueden montar en las distribuciones de Linux con hello [cifs-utils paquete](https://wiki.samba.org/index.php/LinuxCIFS_utils) de hello [proyecto Samba](https://www.samba.org/). Este artículo muestra un recurso compartido de archivos de Azure de toomount de dos maneras: a petición con hello `mount` de comandos y de arranque mediante la creación de una entrada en `/etc/fstab`.

> [!NOTE]  
> En orden toomount un recurso compartido de archivos de Azure fuera Hola región de Azure que se hospeda en, como local o en una región distinta de Azure, Hola SO debe admitir funcionalidad de cifrado de Hola de SMB 3.0. La característica de cifrado de SMB 3.0 para Linux se introdujo en el kernel 4.11. Esta característica permite el montaje de recursos compartidos de Azure File desde el entorno local o una región distinta de Azure. En tiempo de presentación de la publicación, esta funcionalidad ha sido utilizados tooUbuntu desde 16.04 y versiones posteriores.


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a>Requisitos previos para el montaje de un recurso compartido de archivos de Azure paquete cifs-utils hello y Linux
* **Seleccionar una distribución de Linux que se puede tener instalado el paquete de utilidades de cifs Hola**: Microsoft recomienda Hola siguiendo las distribuciones de Linux en la Galería de imágenes de Azure hello:

    * Ubuntu Server 14.04+
    * RHEL 7+
    * CentOS 7+
    * Debian 8
    * openSUSE 13.2+
    * SUSE Linux Enterprise Server 12

* <a id="install-cifs-utils"></a>**Hello cifs-utils paquete está instalado**: Hola cifs-utils puede instalarse mediante el Administrador de paquetes de saludo en la distribución de Linux Hola de su elección. 

    En **Ubuntu** y **Debian-based** distribuciones, usar hello `apt-get` Administrador de paquetes:

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    En **RHEL** y **CentOS**, usar hello `yum` Administrador de paquetes:

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    En **openSUSE**, usar hello `zypper` Administrador de paquetes:

    ```
    sudo zypper install samba*
    ```

    En otras distribuciones, utilice el Administrador de paquetes apropiada de Hola o [compilar desde origen](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).

* **Decidir de permisos de directorios/archivos de hello del recurso compartido montado de Hola**: en los siguientes ejemplos de hello, usamos 0777, toogive leer, escribir y ejecutar los usuarios de tooall de permisos. Puede reemplazarlos por otros [permisos chmod](https://en.wikipedia.org/wiki/Chmod), según prefiera. 

* **Nombre de la cuenta de almacenamiento**: toomount compartir de un archivo de Azure, se necesita Hola nombre de cuenta de almacenamiento de Hola.

* **Clave de la cuenta de almacenamiento**: toomount compartir de un archivo de Azure, se necesita Hola clave de almacenamiento principal (o secundario). Actualmente no se admiten claves SAS para el montaje.

* **Asegúrese de que el puerto 445 está abierto**: SMB se comunica a través del puerto TCP 445 - comprobar toosee si el firewall no bloquea el TCP puertos 445 del equipo cliente.

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a>Montar Hola a petición con recurso compartido de archivos de Azure`mount`
1. **[Instalar el paquete de utilidades de cifs Hola para su distribución de Linux](#install-cifs-utils)**.

2. **Cree una carpeta para el punto de montaje de Hola**: Esto puede realizarse en cualquier lugar en el sistema de archivos de Hola.

    ```
    mkdir mymountpoint
    ```

3. **Use Hola montaje comando toomount hello Azure recurso compartido de archivos**: Recuerde tooreplace `<storage-account-name>`, `<share-name>`, y `<storage-account-key>` con la información adecuada Hola.

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> Cuando haya terminado de usar Hola recurso compartido de archivos de Azure, puede usar `sudo umount ./mymountpoint` recurso compartido de hello toounmount.

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a>Crear un punto de montaje persistente para hello Azure recurso compartido de archivos`/etc/fstab`
1. **[Instalar el paquete de utilidades de cifs Hola para su distribución de Linux](#install-cifs-utils)**.

2. **Cree una carpeta para el punto de montaje de Hola**: Esto puede realizarse en cualquier lugar en el sistema de archivos de hello, pero debe toonote Hola ruta de acceso absoluta carpeta Hola. Hola de ejemplo siguiente crea una carpeta bajo la raíz.

    ```
    sudo mkdir /mymountpoint
    ```

3. **Siguiente Hola de uso de comandos hello tooappend siguen demasiado`/etc/fstab`**: Recuerde tooreplace `<storage-account-name>`, `<share-name>`, y `<storage-account-key>` con la información adecuada Hola.

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> Puede usar `sudo mount -a` toomount recurso compartido de archivos de Azure de hello después de editar `/etc/fstab` en lugar de reiniciar el sistema.

## <a name="feedback"></a>Comentarios
Los usuarios de Linux, dudes toohear del usuario.

Hola almacenamiento de archivos de Azure para el grupo de usuarios de Linux proporciona un foro para usted tooshare comentarios como evaluar y adoptar el almacenamiento de archivos en Linux. Correo electrónico [almacenamiento de archivos de Azure a los usuarios de Linux](mailto:azurefileslinuxusers@microsoft.com) grupo de usuarios de toojoin Hola.

## <a name="next-steps"></a>Pasos siguientes
Consulte los vínculos siguientes para obtener más información acerca Azure File Storage.
* [Referencia de la API REST del servicio de archivos](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [Usar Azure PowerShell con Azure Storage](storage-powershell-guide-full.md)
* [Cómo toouse AzCopy con almacenamiento de Microsoft Azure](storage-use-azcopy.md)
* [Uso de hello CLI de Azure con el almacenamiento de Azure](storage-azure-cli.md#create-and-manage-file-shares)
* [Preguntas más frecuentes](storage-files-faq.md)
* [Solución de problemas](storage-troubleshoot-file-connection-problems.md)
