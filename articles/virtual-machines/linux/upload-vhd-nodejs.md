---
title: aaaUpload una imagen personalizada de Linux con 1.0 de CLI de Azure | Documentos de Microsoft
description: "Crear y cargar un tooAzure de disco duro virtual (VHD) con una imagen personalizada de Linux con modelo de implementación del Administrador de recursos de Hola y Hola 1.0 de CLI de Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a>Cargar y crear una VM Linux de imagen de disco personalizado mediante el uso de hello Azure CLI 1.0
Este artículo muestra cómo tooupload un uso de disco duro virtual (VHD) tooAzure Hola modelo de implementación del Administrador de recursos y crear máquinas virtuales de Linux desde su imagen personalizada. Esta funcionalidad le permite tooinstall y configurar una distribución de Linux tooyour requisitos y, a continuación, usar ese archivo VHD tooquickly crear máquinas virtuales de Azure (VM).


## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola


## <a name="quick-commands"></a>Comandos rápidos
Si necesita tooquickly realizar la tarea hello, Hola después Hola de detalles de la sección base tooupload comandos tooAzure de una máquina virtual. Obtener más información y el contexto de cada paso se encuentran rest Hola de documento de hello, [a partir de aquí](#requirements).

Asegúrese de que dispone de [hello Azure CLI 1.0](../../cli-install-nodejs.md) iniciado la sesión y utilizar el modo de administrador de recursos:

```azurecli
azure config mode arm
```

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Nombres de parámetros de ejemplo incluidos `myResourceGroup`, `mystorageaccount` y `myimages`.

En primer lugar, cree un grupo de recursos. Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `WestUs` ubicación:

```azurecli
azure group create myResourceGroup --location "WestUS"
```

Crear un toohold de cuenta de almacenamiento de los discos virtuales. Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada `mystorageaccount`:

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

Lista de claves de acceso de hello para la cuenta de almacenamiento. Tome nota de `key1`:

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

Crear un contenedor dentro de su cuenta de almacenamiento con la clave de almacenamiento de hello que ha adquirido. Hello en el ejemplo siguiente se crea un contenedor denominado `myimages` mediante el valor de clave de almacenamiento de Hola de `key1`:

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

Por último, cargar el contenedor de toohello de disco duro virtual que creó. Especificar la ruta de acceso local de hello tooyour VHD en `/path/to/disk/mydisk.vhd`:

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

Ahora puede crear una máquina virtual desde el disco virtual cargado [mediante plantillas de Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd). También puede usar Hola CLI mediante la especificación de disco de hello URI tooyour (`--image-urn`). Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` con disco virtual Hola cargado previamente:

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

cuenta de almacenamiento de destino de Hello tiene toobe Hola igual como donde cargar el disco virtual para. También necesita toospecify o responder a peticiones de, todos los parámetros adicionales requeridos por Hola de Hola `azure vm create` comando como la red virtual, la dirección IP pública, nombre de usuario y las claves de SSH. Puede leer más sobre hello [disponibles parámetros del Administrador de recursos de CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

## <a name="requirements"></a>Requisitos
Hola toocomplete siguiendo los pasos, debe:

* **Sistema operativo Linux instalado en un archivo .vhd** -instalar un [distribución de Linux están aprobados Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (o consulte [información para las distribuciones no aprobadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa disco virtual en hello VHD formato. Varias herramientas existen toocreate una máquina virtual y el disco duro virtual:
  * Instalar y configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), teniendo cuidado de toouse del disco duro virtual como el formato de imagen. Si es necesario, puede [convertir una imagen](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) con `qemu-img convert`.
  * También puede usar Hyper-V [en Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [en Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> no se admite el formato VHDX más reciente de Hello en Azure. Cuando se crea una máquina virtual, especifique VHD como formato de Hola. Si es necesario, se puede convertir VHDX discos tooVHD con [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet de PowerShell. Además, Azure no permite cargar discos duros virtuales dinámicos, por lo que necesita tooconvert tal toostatic discos VHD antes de cargar. Puede usar herramientas como [utilidades de disco duro virtual de Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert discos dinámicos durante el proceso de Hola de carga tooAzure.
> 
> 

* Creado a partir de la imagen personalizada de las máquinas virtuales deben residir en hello misma cuenta de almacenamiento que la propia imagen de Hola
  * Crear un toohold de cuenta y el contenedor de almacenamiento tanto la imagen personalizada y crear máquinas virtuales
  * Una vez que haya creado todas las máquinas virtuales, puede eliminar su imagen de forma segura.

Asegúrese de que dispone de [hello Azure CLI 1.0](../../cli-install-nodejs.md) iniciado la sesión y utilizar el modo de administrador de recursos:

```azurecli
azure config mode arm
```

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Nombres de parámetros de ejemplo incluidos `myResourceGroup`, `mystorageaccount` y `myimages`.

<a id="prepimage"></a>

## <a name="prepare-hello-image-toobe-uploaded"></a>Preparar Hola imagen toobe cargado
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


## <a name="create-a-resource-group"></a>Crear un grupo de recursos
Grupos de recursos lógicamente reunir todos los toosupport de recursos de Azure de hello las máquinas virtuales, como una red virtual Hola y el almacenamiento. Lea más sobre [grupos de recursos de Azure aquí](../../azure-resource-manager/resource-group-overview.md). Antes de cargar la imagen de disco personalizado y crear máquinas virtuales, primero debe toocreate un grupo de recursos. 

Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `WestUS` ubicación:

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a>Crear una cuenta de almacenamiento
Las máquinas virtuales se almacenan como blobs en páginas dentro de una cuenta de almacenamiento. Lea más sobre [almacenamiento de blobs de Azure aquí](../../storage/common/storage-introduction.md#blob-storage). Creará una cuenta de almacenamiento para la imagen de disco personalizada y las máquinas virtuales. Todas las máquinas virtuales que se crean desde su toobe de necesidad de imagen de disco personalizado en hello la misma cuenta de almacenamiento que esa imagen.

Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada `mystorageaccount` en grupo de recursos de hello creado anteriormente:

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a>Enumerar claves de cuentas de almacenamiento
Azure genera dos claves de acceso de 512 bits para cada cuenta de almacenamiento. Estas teclas de acceso se utilizan para autenticar la cuenta de almacenamiento de toohello, como toocarry operaciones de escritura de salida. Obtenga más información sobre [administrar acceso toostorage aquí](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Puede ver las teclas de acceso con hello `azure storage account keys list` comando.

Ver las teclas de acceso de Hola Hola cuenta de almacenamiento que creó:

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
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
Hola igual que crear directorios distintos toologically organizar el sistema de archivos local, crear contenedores dentro de un tooorganize de cuenta de almacenamiento, las imágenes y discos virtuales. Una cuenta de almacenamiento puede contener un número cualquiera de contenedores. 

Hello en el ejemplo siguiente se crea un contenedor denominado `myimages`, especificar la clave de acceso de hello obtenido en el paso anterior de hello (`key1`):

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a>Carga de VHD
Ahora, en realidad, puede cargar la imagen de disco personalizada. Al igual que con todos los discos virtuales usados por las máquinas virtuales, cargará y almacenará la imagen de disco personalizada como un blob en páginas.

Especifique la clave de acceso, el contenedor de Hola que creó en el paso anterior de Hola y Hola, a continuación, la imagen de disco personalizada toohello de ruta de acceso en el equipo local:

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a>Creación de una máquina virtual a partir de una imagen personalizada
Al crear máquinas virtuales desde su imagen de disco personalizado, especifique la imagen de disco de toohello URI de Hola. Asegúrese de que Hola coincidencias de cuenta de almacenamiento de destino donde se almacena la imagen de disco personalizada. Puede crear la máquina virtual con la plantilla de CLI de Azure o el Administrador de recursos JSON Hola.

### <a name="create-a-vm-using-hello-azure-cli"></a>Crear una máquina virtual mediante Hola CLI de Azure
Especificar hello `--image-urn` parámetro con hello `azure vm create` imagen de disco personalizada de comando toopoint tooyour. Asegúrese de que `--storage-account-name` coincidencias Hola cuenta de almacenamiento donde se almacena la imagen de disco personalizada. No es necesario toouse Hola mismo contenedor como Hola toostore de imagen de disco personalizada las máquinas virtuales. Realizar toocreate seguro de los contenedores adicionales en hello misma manera que Hola pasos anteriores antes de cargar las imágenes de disco personalizadas.

Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` desde la imagen de disco personalizado:

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

Todavía necesita toospecify o responder a peticiones de, todos los parámetros adicionales requeridos por Hola de Hola `azure vm create` comando como la red virtual, la dirección IP pública, nombre de usuario y las claves de SSH. Obtener más información acerca de hello [disponibles parámetros del Administrador de recursos de CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

### <a name="create-a-vm-using-a-json-template"></a>Creación de una máquina virtual con una plantilla JSON
Plantillas de administrador de recursos de Azure son archivos de JavaScript Object Notation (JSON) que definen el entorno de hello desea toobuild. plantillas de Hola se desglosan en proveedores de recursos de toodifferent como compute o red. Puede usar las plantillas existentes o escribir las suyas propias. Lea más sobre el [uso de Resource Manager y las plantillas](../../azure-resource-manager/resource-group-overview.md).

Dentro de hello `Microsoft.Compute/virtualMachines` proveedor de la plantilla, tendrá un `storageProfile` nodo que contiene los detalles de configuración de hello para la máquina virtual. Hola dos parámetros principales tooedit son hello `image` y `vhd` URI que señalan a imágenes de disco personalizadas tooyour y disco virtual de la máquina virtual nueva. siguiente Hello muestra un ejemplo de Hola JSON para el uso de una imagen de disco personalizado:

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

Puede usar [esta toocreate de plantilla existente una máquina virtual desde una imagen personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) o leer acerca de [crear sus propias plantillas de Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md). 

Una vez que tenga una plantilla configurada, crear las máquinas virtuales con hello `azure group deployment create` comando. Especificar Hola URI de la plantilla JSON con hello `--template-uri` parámetro:

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

Si tiene un archivo JSON que se almacena localmente en el equipo, puede usar hello `--template-file` parámetro en su lugar:

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>Pasos siguientes
Después de haber preparado y cargado el disco virtual personalizado, puede leer más sobre el [uso de Resource Manager y las plantillas](../../azure-resource-manager/resource-group-overview.md). Puede que también desee demasiado[agregar un disco de datos](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nuevas máquinas virtuales. Si tiene aplicaciones que se ejecutan en las máquinas virtuales que necesite tooaccess, asegúrese de demasiado[puertos abiertos y los puntos de conexión](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

