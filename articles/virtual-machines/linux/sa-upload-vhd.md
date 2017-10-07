---
title: un disco de Linux personalizado con Azure CLI 2.0 aaaUpload | Documentos de Microsoft
description: "Crear y cargar un tooAzure de disco duro virtual (VHD) mediante el modelo de implementación del Administrador de recursos de Hola y Hola 2.0 de CLI de Azure"
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
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Cargar y crear una VM Linux desde disco personalizado con hello 2.0 de CLI de Azure
Este artículo muestra cómo tooupload una tooan de disco duro virtual (VHD) el almacenamiento de Azure cuenta con hello 2.0 de CLI de Azure y crear máquinas virtuales de Linux desde este disco personalizado. También puede realizar estos pasos con hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Esta funcionalidad le permite tooinstall y configurar una distribución de Linux tooyour requisitos y, a continuación, usar ese archivo VHD tooquickly crear máquinas virtuales de Azure (VM).

En este tema usa las cuentas de almacenamiento para hello finales discos duros virtuales, pero también puede realizar estos pasos con [discos administrados por](upload-vhd.md). 

## <a name="quick-commands"></a>Comandos rápidos
Si necesita tooquickly realizar la tarea hello, Hola después Hola de detalles de la sección base tooupload comandos tooAzure de un disco duro virtual. Obtener más información y el contexto de cada paso se encuentran rest Hola de documento de hello, [a partir de aquí](#requirements).

Asegúrese de que tiene más reciente hello [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Nombres de parámetros de ejemplo incluidos `myResourceGroup`, `mystorageaccount` y `mydisks`.

En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `WestUs` ubicación:

```azurecli
az group create --name myResourceGroup --location westus
```

Crear un toohold de cuenta de almacenamiento de los discos virtuales con [crear cuenta de almacenamiento az](/cli/azure/storage/account#create). Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada `mystorageaccount`:

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

Lista de claves de acceso de Hola para su cuenta de almacenamiento con [lista de claves de cuenta de almacenamiento az](/cli/azure/storage/account/keys#list). Tome nota de `key1`:

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

Crear un contenedor dentro de su cuenta de almacenamiento con la clave de almacenamiento de hello obtenido con [crear contenedor de almacenamiento az](/cli/azure/storage/container#create). Hello en el ejemplo siguiente se crea un contenedor denominado `mydisks` mediante el valor de clave de almacenamiento de Hola de `key1`:

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

Por último, cargar el contenedor de toohello de disco duro virtual que creó con [carga de blobs de almacenamiento az](/cli/azure/storage/blob#upload). Especificar la ruta de acceso local de hello tooyour VHD en `/path/to/disk/mydisk.vhd`:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

Especifique Hola URI tooyour disco (`--image`) con [crear vm az](/cli/azure/vm#create). Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` con disco virtual Hola cargado previamente:

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

cuenta de almacenamiento de destino de Hello tiene toobe Hola igual como donde cargar el disco virtual para. También necesita toospecify o responder a peticiones de, todos los parámetros adicionales requeridos por Hola de Hola **crear vm az** comando como la red virtual, la dirección IP pública, nombre de usuario y las claves de SSH. Puede leer más sobre hello [disponibles parámetros del Administrador de recursos de CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

## <a name="requirements"></a>Requisitos
Hola toocomplete siguiendo los pasos, debe:

* **Sistema operativo Linux instalado en un archivo .vhd** -instalar un [distribución de Linux están aprobados Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (o consulte [información para las distribuciones no aprobadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa disco virtual en hello VHD formato. Varias herramientas existen toocreate una máquina virtual y el disco duro virtual:
  * Instalar y configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), teniendo cuidado de toouse del disco duro virtual como el formato de imagen. Si es necesario, puede [convertir una imagen](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) con `qemu-img convert`.
  * También puede usar Hyper-V [en Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [en Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> no se admite el formato VHDX más reciente de Hello en Azure. Cuando se crea una máquina virtual, especifique VHD como formato de Hola. Si es necesario, se puede convertir VHDX discos tooVHD con [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet de PowerShell. Además, Azure no permite cargar discos duros virtuales dinámicos, por lo que necesita tooconvert tal toostatic discos VHD antes de cargar. Puede usar herramientas como [utilidades de disco duro virtual de Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert discos dinámicos durante el proceso de Hola de carga tooAzure.
> 
> 

* Máquinas virtuales creadas a partir del disco personalizado deben residir en hello misma cuenta de almacenamiento como el propio disco Hola
  * Crear un toohold de cuenta y el contenedor de almacenamiento del disco personalizado y creado las máquinas virtuales
  * Una vez que haya creado todas las máquinas virtuales, puede eliminar el disco de forma segura.

Asegúrese de que tiene más reciente hello [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Nombres de parámetros de ejemplo incluidos `myResourceGroup`, `mystorageaccount` y `mydisks`.

<a id="prepimage"></a>

## <a name="prepare-hello-disk-toobe-uploaded"></a>Preparar Hola disco toobe cargado
Azure admite varias distribuciones Linux (consulte [Distribuciones aprobadas](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Hola siguientes artículos guiarle por cómo tooprepare Hola diversas distribuciones de Linux que se admiten en Azure:

* **[Distribuciones basadas en CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES y openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Otras distribuciones no aprobadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

Consulte también hello  **[notas sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes)**  para obtener más sugerencias sobre cómo preparar imágenes de Linux de Azure.

> [!NOTE]
> Hola [plataforma Windows Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) aplica tooVMs ejecutando Linux sólo cuando uno de hello están aprobados distribuciones se utilizan con los detalles de configuración de hello tal como se especifica en 'Admite versiones' en [Linux en Azure aprobadas Distribuciones](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

## <a name="create-a-resource-group"></a>Crear un grupo de recursos
Grupos de recursos lógicamente reunir todos los toosupport de recursos de Azure de hello las máquinas virtuales, como una red virtual Hola y el almacenamiento. Para más información acerca de los grupos de recursos, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Antes de cargar el disco personalizado y crear máquinas virtuales, primero debe toocreate un grupo de recursos con [crear grupo az](/cli/azure/group#create).

Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westus` ubicación:

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a>Crear una cuenta de almacenamiento

Cree una cuenta de almacenamiento para el disco personalizado y las máquinas virtuales con [az storage account create](/cli/azure/storage/account#create). Todas las máquinas virtuales con discos no administrados que se crean desde su toobe de necesidad de disco personalizado en hello misma cuenta de almacenamiento que dicho disco. 

Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada `mystorageaccount` en grupo de recursos de hello creado anteriormente:

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a>Enumerar claves de cuentas de almacenamiento
Azure genera dos claves de acceso de 512 bits para cada cuenta de almacenamiento. Estas teclas de acceso se utilizan para autenticar la cuenta de almacenamiento de toohello, como toocarry operaciones de escritura de salida. Obtenga más información sobre [administrar acceso toostorage aquí](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Ver las teclas de acceso de hello con [lista de claves de cuenta de almacenamiento az](/cli/azure/storage/account/keys#list).

Ver las teclas de acceso de Hola Hola cuenta de almacenamiento que creó:

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
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
Tome nota del `key1` tal y como se va a utilizar se toointeract con su cuenta de almacenamiento en los pasos siguientes de Hola.

## <a name="create-a-storage-container"></a>Creación de un contenedor de almacenamiento
Hola igual que crear directorios distintos toologically organizar el sistema de archivos local, crear contenedores dentro de un tooorganize de cuenta de almacenamiento de los discos. Una cuenta de almacenamiento puede contener un número cualquiera de contenedores. Cree un contenedor con [az storage container create](/cli/azure/storage/container#create).

Hello en el ejemplo siguiente se crea un contenedor denominado `mydisks`:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a>Carga de VHD
Ahora puede cargar su disco personalizado con [az storage blob upload](/cli/azure/storage/blob#upload). Cargue y almacene el disco personalizado como un blob en páginas.

Especifique la clave de acceso, el contenedor de Hola que creó en el paso anterior de hello y, a continuación, Hola disco personalizado de toohello de ruta de acceso en el equipo local:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a>Crear hello VM
toocreate una máquina virtual con discos no administrados, especifique el disco de tooyour URI de hello (`--image`) con [crear vm az](/cli/azure/vm#create). Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` con disco virtual Hola cargado previamente:

Especificar hello `--image` parámetro con [crear vm az](/cli/azure/vm#create) toopoint tooyour personalizado disco. Asegúrese de que `--storage-account` coincidencias Hola cuenta de almacenamiento donde se almacena el disco personalizado. No es necesario toouse Hola mismo contenedor como Hola disco personalizada toostore las máquinas virtuales. Realizar toocreate seguro de los contenedores adicionales en hello misma manera que Hola pasos anteriores antes de cargar el disco personalizado.

Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` desde el disco personalizado:

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

Todavía necesita toospecify o responder a peticiones de, todos los parámetros adicionales requeridos por Hola de Hola **crear vm az** comando como nombre de usuario y las claves SSH.


## <a name="resource-manager-template"></a>Plantilla de Resource Manager
Plantillas de administrador de recursos de Azure son archivos de JavaScript Object Notation (JSON) que definen el entorno de hello desea toobuild. plantillas de Hola se desglosan en proveedores de recursos de toodifferent como compute o red. Puede usar las plantillas existentes o escribir las suyas propias. Lea más sobre el [uso de Resource Manager y las plantillas](../../azure-resource-manager/resource-group-overview.md).

Dentro de hello `Microsoft.Compute/virtualMachines` proveedor de la plantilla, tendrá un `storageProfile` nodo que contiene los detalles de configuración de hello para la máquina virtual. Hola dos parámetros principales tooedit son hello `image` y `vhd` URI que apuntan al disco personalizada tooyour y disco virtual de la máquina virtual nueva. siguiente Hello muestra un ejemplo de Hola JSON para usar un disco personalizado:

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

Puede usar [esta toocreate de plantilla existente una máquina virtual desde una imagen personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) o leer acerca de [crear sus propias plantillas de Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md). 

Una vez que tenga una plantilla configurada, utilice [Crear implementación de grupo az](/cli/azure/group/deployment#create) toocreate las máquinas virtuales. Especificar Hola URI de la plantilla JSON con hello `--template-uri` parámetro:

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

Si tiene un archivo JSON que se almacena localmente en el equipo, puede usar hello `--template-file` parámetro en su lugar:

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>Pasos siguientes
Después de haber preparado y cargado el disco virtual personalizado, puede leer más sobre el [uso de Resource Manager y las plantillas](../../azure-resource-manager/resource-group-overview.md). Puede que también desee demasiado[agregar un disco de datos](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nuevas máquinas virtuales. Si tiene aplicaciones que se ejecutan en las máquinas virtuales que necesite tooaccess, asegúrese de demasiado[puertos abiertos y los puntos de conexión](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

