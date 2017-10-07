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
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a>Montaje de Azure File Storage en VM Linux mediante SMB con la CLI de Azure 1.0

Este artículo muestra cómo toomount almacenamiento de archivos de Azure en una VM de Linux mediante el uso de Hola protocolo de bloque de mensajes del servidor (SMB). Almacenamiento de archivos ofrece recursos compartidos de archivos en la nube de Hola a través del protocolo SMB estándar de Hola. Hola requisitos son:

* Una [cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/)
* [Archivos de clave pública y privada Secure Shell (SSH)](mac-create-ssh-keys.md)

## <a name="cli-versions-toouse"></a>Toouse de versiones CLI
Puede completar la tarea hello mediante uno de hello después de versiones de la interfaz de línea de comandos (CLI):

- [Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola


## <a name="quick-commands"></a>Comandos rápidos
tarea de hello tooaccomplish rápidamente, siga los pasos de hello en esta sección. Para obtener más información y el contexto, comienzan en hello ["Tutorial detallado"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) sección.

### <a name="prerequisites"></a>Requisitos previos
* Un grupo de recursos
* Una red virtual de Azure
* Un grupo de seguridad de red con un SSH entrante
* Una subred
* Una cuenta de almacenamiento de Azure
* Claves de cuenta de almacenamiento de Azure
* Un recurso compartido de Azure File Storage
* Una VM Linux

Reemplace los ejemplos por su propia configuración.

### <a name="create-a-directory-for-hello-local-mount"></a>Cree un directorio de montaje local Hola

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a>Hola archivo almacenamiento SMB recurso compartido toohello montaje punto de montaje

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a>Conservar el montaje de hello tras un reinicio.
Agregar Hola siguen demasiado`/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Tutorial detallado

Almacenamiento de archivos ofrece recursos compartidos de archivos en la nube de Hola que utilizan el protocolo SMB estándar de Hola. Con la versión más reciente de Hola de almacenamiento de archivos, también se puede montar un recurso compartido de archivos desde cualquier sistema operativo que admite SMB 3.0. Cuando se usa un montaje SMB en Linux, obtendrá las copias de seguridad fácil tooa robustas y permanente archivado ubicación de almacenamiento que es compatible con un SLA.

Mover archivos de un montaje SMB tooan de máquina virtual que se hospeda en el almacenamiento de archivos es que una excelente manera toodebug registros. Esto es así porque Hola recurso compartido SMB mismo se puede montar localmente tooyour Mac, Linux o Windows estación de trabajo. SMB no es la mejor solución para la transmisión por secuencias Linux de Hola o registros de aplicación en tiempo real, porque Hola protocolo SMB no se generan toohandle tales derechos de registro pesada. Una herramienta de nivel de registro unificado dedicada como Fluentd sería una opción mejor que SMB para recopilar la salida de registro de la aplicación y Linux.

Para este tutorial detallado, creamos requisitos previos de hello necesario toofirst crear recurso compartido de almacenamiento de archivos de hello y, a continuación, monte a través de SMB en una VM de Linux.

1. Crear una cuenta de almacenamiento de Azure mediante el siguiente código de hello:

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. Mostrar claves de cuenta de almacenamiento de Hola.

    Cuando se crea una cuenta de almacenamiento, se crean las claves de cuenta de hello en pares para que se pueden girar sin ninguna interrupción del servicio. Cuando cambie toohello segunda clave en el par de hello, cree un nuevo par de claves. Nuevas claves de cuenta de almacenamiento se crean siempre en pares y asegurarse de que siempre tiene al menos un almacenamiento sin usar de tooswitch listo clave a. claves de cuenta de almacenamiento de hello tooshow, usar hello siguiente código:

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. Crear recurso compartido de almacenamiento de archivos de Hola.

    recurso compartido de almacenamiento de archivos de Hello contiene el recurso compartido SMB de Hola. cuota de Hello siempre se expresa en gigabytes (GB). toocreate Hola recurso compartido de almacenamiento de archivos, usar hello siguiente código:

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. Crear el directorio de punto de montaje de Hola.

    Debe crear un directorio local en Hola Hola Linux archivo sistema toomount recurso compartido de SMB. Algo escrito o leer desde el directorio de montaje local Hola se reenvía toohello recurso compartido SMB que se hospeda en el almacenamiento de archivos. directorio de hello toocreate, Hola de uso siguiente código:

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. Montar Hola recurso compartido SMB mediante el uso de hello siguiente código:

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. Conservar Hola montar SMB a través de reinicios.

    Al reiniciar Hola VM de Linux, hello montada de recurso compartido SMB se desmonta durante el cierre. tooremount Hola recurso compartido SMB de arranque, debe agregar una toohello línea Linux/etc/fstab. Linux utiliza Hola fstab archivo toolist Hola sistemas de archivos que necesita toomount durante el proceso de arranque de Hola. Agregar recurso compartido SMB Hola garantiza que ese recurso compartido de archivo almacenamiento hello es un sistema de archivos montado permanentemente para hello VM de Linux. Agregar tooa del recurso compartido SMB de hello archivo almacenamiento nueva máquina virtual es posible cuando se usa en la nube init.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Pasos siguientes

- [Uso de nube init toocustomize una VM de Linux durante la creación](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Agregar una VM de Linux tooa de disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Cifrar los discos en una VM Linux mediante Hola CLI de Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
