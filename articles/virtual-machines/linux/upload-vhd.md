---
title: aaaUpload o copia una VM de Linux personalizado con 2.0 de CLI de Azure | Documentos de Microsoft
description: "Cargar o copiar una máquina virtual personalizada utilizando el modelo de implementación del Administrador de recursos de Hola y Hola 2.0 de CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Crear una VM Linux desde disco personalizado con hello 2.0 de CLI de Azure

<!-- rename toocreate-vm-specialized -->

Este artículo muestra cómo tooupload un disco duro virtual (VHD) personalizado o copiar un un disco duro virtual existente en Azure y crear nuevas máquinas virtuales de Linux (VM) desde el disco de saludo personalizado. Puede instalar y configurar una distribución de Linux tooyour requisitos y, a continuación, usar ese archivo VHD tooquickly crear una nueva máquina virtual de Azure.

Si desea toocreate varias máquinas virtuales desde el disco personalizado, debe crear una imagen de la máquina virtual o un disco duro virtual. Para obtener más información, consulte [crear una imagen personalizada de una máquina virtual de Azure con hello CLI](tutorial-custom-images.md).

Tiene dos opciones:
* [Carga de un disco duro virtual](#option-1-upload-a-specialized-vhd)
* [Copia de una máquina virtual de Azure existente](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a>Comandos rápidos

Al crear una nueva máquina virtual mediante [crear vm az](/cli/azure/vm#create) desde un disco personalizado o especializado **adjuntar** disco hello (--adjuntar-os-disk) en lugar de especificar una imagen personalizada o marketplace (--imagen). Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM* mediante Hola administrado disco llamado *myManagedDisk* creado a partir de un VHD personalizado:

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a>Requisitos
Hola toocomplete siguiendo los pasos, debe:

* Una máquina virtual Linux que se ha preparado para su uso en Azure. Hola [preparar Hola VM](#prepare-the-vm) sección de este artículo trata sobre cómo toofind distribución información específica acerca de cómo instalar Hola agente de Linux de Azure (waagent) que es necesario para hello VM toowork correctamente en Azure y para toobe pueda tooconnect tooit mediante SSH.
* archivo de disco duro virtual de Hello desde una existente [distribución de Linux están aprobados Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (o consulte [información para las distribuciones no aprobadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa disco virtual en formato de disco duro virtual de Hola. Varias herramientas existen toocreate una máquina virtual y el disco duro virtual:
  * Instalar y configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), teniendo cuidado de toouse del disco duro virtual como el formato de imagen. Si es necesario, puede [convertir una imagen](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) con **qemu-img convert**.
  * También puede usar Hyper-V [en Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [en Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> no se admite el formato VHDX más reciente de Hello en Azure. Cuando se crea una máquina virtual, especifique VHD como formato de Hola. Si es necesario, se puede convertir VHDX discos tooVHD con [convertir img qemu](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) cmdlet de PowerShell. Además, Azure no permite cargar discos duros virtuales dinámicos, por lo que necesita tooconvert tal toostatic discos VHD antes de cargar. Puede usar herramientas como [utilidades de disco duro virtual de Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert discos dinámicos durante el proceso de Hola de carga tooAzure.
> 
> 


* Asegúrese de que tiene más reciente hello [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *mystorageaccount* y *mydisks*.

<a id="prepimage"></a>

## <a name="prepare-hello-vm"></a>Preparar Hola VM

Azure admite varias distribuciones Linux (consulte [Distribuciones aprobadas](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Hola siguientes artículos guiarle por cómo tooprepare Hola diversas distribuciones de Linux que se admiten en Azure:

* [Distribuciones basadas en CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SLES y openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Otras distribuciones no aprobadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Consulte también hello [notas sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes) para obtener más sugerencias sobre cómo preparar imágenes de Linux de Azure.

> [!NOTE]
> Hola [plataforma Windows Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) aplica tooVMs ejecutando Linux sólo cuando uno de hello están aprobados distribuciones se utilizan con los detalles de configuración de hello tal como se especifica en 'Admite versiones' en [Linux en Azure aprobadas Distribuciones](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

## <a name="option-1-upload-a-vhd"></a>Opción 1: Cargar un disco duro virtual

Puede cargar un VHD personalizado que se esté ejecutando en un equipo local o que se haya exportado desde otra nube. toouse Hola VHD toocreate una nueva máquina virtual de Azure, necesita almacenamiento de tooa de disco duro virtual de hello tooupload cuenta y crear un disco administrado desde Hola VHD. 

### <a name="create-a-resource-group"></a>Crear un grupo de recursos

Antes de cargar el disco personalizado y crear máquinas virtuales, primero debe toocreate un grupo de recursos con [crear grupo az](/cli/azure/group#create).

Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación: [información general de discos administrado de Azure](../windows/managed-disks-overview.md)
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a>Crear una cuenta de almacenamiento

Cree una cuenta de almacenamiento para el disco personalizado y las máquinas virtuales con [az storage account create](/cli/azure/storage/account#create). 

Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada *mystorageaccount* en grupo de recursos de hello creado anteriormente:

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a>Enumerar claves de cuentas de almacenamiento
Azure genera dos claves de acceso de 512 bits para cada cuenta de almacenamiento. Estas teclas de acceso se utilizan para autenticar la cuenta de almacenamiento toohello, al igual que lleve a cabo operaciones de escritura. Obtenga más información sobre [administrar acceso toostorage aquí](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Ver las teclas de acceso de hello con [lista de claves de cuenta de almacenamiento az](/cli/azure/storage/account/keys#list).

Ver las teclas de acceso de Hola Hola cuenta de almacenamiento que creó:

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

es similar a la salida de Hello:

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
Tome nota del **key1** tal y como se va a utilizar se toointeract con su cuenta de almacenamiento en los pasos siguientes de Hola.

### <a name="create-a-storage-container"></a>Creación de un contenedor de almacenamiento
Hola igual que crear directorios distintos toologically organizar el sistema de archivos local, crear contenedores dentro de un tooorganize de cuenta de almacenamiento de los discos. Una cuenta de almacenamiento puede contener un número cualquiera de contenedores. Cree un contenedor con [az storage container create](/cli/azure/storage/container#create).

Hello en el ejemplo siguiente se crea un contenedor denominado *mydisks*:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a>Cargar Hola VHD
Ahora puede cargar su disco personalizado con [az storage blob upload](/cli/azure/storage/blob#upload). Cargue y almacene el disco personalizado como un blob en páginas.

Especifique la clave de acceso, el contenedor de Hola que creó en el paso anterior de hello y, a continuación, Hola disco personalizado de toohello de ruta de acceso en el equipo local:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
Hola cargar VHD puede tardar un rato.

### <a name="create-a-managed-disk"></a>Creación de un disco administrado


Crear un disco administrado del uso de disco duro virtual de hello [crear disco az](/cli/azure/disk#create). Hello en el ejemplo siguiente se crea un disco administrado llamado *myManagedDisk* de hello VHD cargado tooyour denominada cuenta de almacenamiento y contenedor:

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a>Opción 2: Copiar una máquina virtual existente

También puede crear Hola personalizada VM en Azure y, a continuación, copiar el disco de SO de Hola y adjuntarlo tooa nueva VM toocreate otra copia. Esto es correcto para la prueba, pero si desea toouse una VM de Azure existente como modelo de Hola para varias máquinas virtuales nuevas, realmente debe crear un **imagen** en su lugar. Para obtener más información acerca de cómo crear una imagen de una máquina virtual de Azure existente, vea [crear una imagen personalizada de una máquina virtual de Azure con hello CLI](tutorial-custom-images.md)

### <a name="create-a-snapshot"></a>Crear una instantánea

En este ejemplo se crea una instantánea de una máquina virtual denominada *myVM* en el grupo de recursos *myResourceGroup* y se crea una instantánea denominada *osDiskSnapshot*.

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a>Crear disco administrado Hola

Crear un nuevo disco administrado desde la instantánea de Hola.

Obtener Id. de Hola de instantánea de Hola. En este ejemplo, se denomina instantánea hello *osDiskSnapshot* y se encuentra en hello *myResourceGroup* grupo de recursos.

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

Crear disco administrado Hola. En este ejemplo se va a crear un disco administrado denominado *myManagedDisk* a partir de la instantánea, que tiene un tamaño de 128 GB de almacenamiento estándar.

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a>Crear hello VM

Ahora, cree la máquina virtual con [crear vm az](/cli/azure/vm#create) y adjuntar (--adjuntar-os-disk) Hola administrados disco como disco de SO Hola. Hello en el ejemplo siguiente se crea una máquina virtual denominada *myNewVM* mediante Hola administrado disco creado a partir de su disco duro virtual cargado:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

Debe ser capaz de tooSSH en hello VM con credenciales de Hola desde una VM de origen Hola. 

## <a name="next-steps"></a>Pasos siguientes
Después de haber preparado y cargado el disco virtual personalizado, puede leer más sobre el [uso de Resource Manager y las plantillas](../../azure-resource-manager/resource-group-overview.md). Puede que también desee demasiado[agregar un disco de datos](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nuevas máquinas virtuales. Si tiene aplicaciones que se ejecutan en las máquinas virtuales que necesite tooaccess, asegúrese de demasiado[puertos abiertos y los puntos de conexión](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

