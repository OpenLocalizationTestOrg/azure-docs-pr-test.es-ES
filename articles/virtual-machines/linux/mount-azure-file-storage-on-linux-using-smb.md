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
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a>Montaje de Azure File Storage en máquinas virtuales Linux con SMB

Este artículo muestra cómo montar hello tooutilize servicio de almacenamiento de archivos de Azure en una VM de Linux con SMB con hello 2.0 de CLI de Azure. Almacenamiento de archivos de Azure ofrece recursos compartidos de archivos en la nube de hello mediante el protocolo SMB estándar de Hola. También puede realizar estos pasos con hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Hola requisitos son:

- [una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/);
- [archivos de clave SSH pública y privada](mac-create-ssh-keys.md).

## <a name="quick-commands"></a>Comandos rápidos

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
toodo por lo tanto, agregar Hola después línea toohello `/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Tutorial detallado

Almacenamiento de archivos ofrece recursos compartidos de archivos en la nube de Hola que utilizan el protocolo SMB estándar de Hola. Con la versión más reciente de Hola de almacenamiento de archivos, también se puede montar un recurso compartido de archivos desde cualquier sistema operativo que admite SMB 3.0. Cuando se usa un montaje SMB en Linux, obtendrá las copias de seguridad fácil tooa robustas y permanente archivado ubicación de almacenamiento que es compatible con un SLA.

Mover archivos de un montaje SMB tooan de máquina virtual que se hospeda en el almacenamiento de archivos es que una excelente manera toodebug registros. Esto es así porque Hola recurso compartido SMB mismo se puede montar localmente tooyour Mac, Linux o Windows estación de trabajo. SMB no es la mejor solución para la transmisión por secuencias Linux de Hola o registros de aplicación en tiempo real, porque Hola protocolo SMB no se generan toohandle tales derechos de registro pesada. Una herramienta de nivel de registro unificado dedicada como Fluentd sería una opción mejor que SMB para recopilar la salida de registro de la aplicación y Linux.

Para este tutorial detallado, creamos requisitos previos de hello necesario toofirst crear recurso compartido de almacenamiento de archivos de hello y, a continuación, monte a través de SMB en una VM de Linux.

1. Crear un grupo de recursos con [crear grupo az](/cli/azure/group#create) recurso compartido de archivos de toohold Hola.

    toocreate un grupo de recursos denominado `myResourceGroup` en la ubicación de "West US" Hola, usar hello siguiente ejemplo:

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. Crear una cuenta de almacenamiento de Azure con [crear cuenta de almacenamiento az](/cli/azure/storage/account#create) toostore Hola archivos reales.

    toocreate una cuenta de almacenamiento denominado mystorageaccount mediante hello Standard_LRS almacenamiento SKU, Hola de uso siguiente ejemplo:

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. Mostrar claves de cuenta de almacenamiento de Hola.

    Cuando se crea una cuenta de almacenamiento, se crean las claves de cuenta de hello en pares para que se pueden girar sin ninguna interrupción del servicio. Cuando cambie toohello segunda clave en el par de hello, cree un nuevo par de claves. Nuevas claves de cuenta de almacenamiento se crean siempre en pares, garantizando así que siempre tenga al menos un almacenamiento sin usar cuenta tooswitch clave listo para.

    Ver claves de cuenta de almacenamiento de hello con hello [lista de claves de cuenta de almacenamiento az](/cli/azure/storage/account/keys#list). Hola claves de cuenta de almacenamiento para hello denominado `mystorageaccount` se muestran en el siguiente ejemplo de Hola:

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    tooextract una clave única, utilice hello `--query` marca. Hello en el ejemplo siguiente se extrae primera clave de hello (`[0]`):

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. Crear recurso compartido de almacenamiento de archivos de Hola.

    recurso compartido de almacenamiento de archivos de Hello contiene Hola con recurso compartido SMB [crear recurso compartido de almacenamiento az](/cli/azure/storage/share#create). cuota de Hello siempre se expresa en gigabytes (GB). Pasar de una de las claves de Hola de hello anterior `az storage account keys list` comando. Crear un recurso compartido denominado mystorageshare con una cuota de 10 GB mediante el siguiente ejemplo de Hola:

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. Cree un directorio de punto de montaje.

    Cree un directorio local en Hola Hola Linux archivo sistema toomount recurso compartido de SMB. Algo escrito o leer desde el directorio de montaje local Hola se reenvía toohello recurso compartido SMB que se hospeda en el almacenamiento de archivos. toocreate un directorio local en/mnt/mymountdirectory, Hola de uso siguiente ejemplo:

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. Montar el directorio local del toohello de recurso compartido SMB Hola.

    Proporcionar su propio nombre de usuario de cuenta de almacenamiento y la clave de cuenta de almacenamiento para las credenciales de montaje de hello como sigue:

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. Conservar Hola montar SMB a través de reinicios.

    Al reiniciar Hola VM de Linux, hello montada de recurso compartido SMB se desmonta durante el cierre. Hola tooremount recurso compartido SMB en el arranque, agregar un toohello línea Linux/etc/fstab. Linux utiliza Hola fstab archivo toolist Hola sistemas de archivos que necesita toomount durante el proceso de arranque de Hola. Agregar recurso compartido SMB Hola garantiza que ese recurso compartido de archivo almacenamiento hello es un sistema de archivos montado permanentemente para hello VM de Linux. Agregar tooa del recurso compartido SMB de hello archivo almacenamiento nueva máquina virtual es posible cuando se usa en la nube init.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Pasos siguientes

- [Uso de nube init toocustomize una VM de Linux durante la creación](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Agregar una VM de Linux tooa de disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Cifrar los discos en una VM Linux mediante Hola CLI de Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
