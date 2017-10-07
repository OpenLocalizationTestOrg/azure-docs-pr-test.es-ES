---
title: aaaCreate y cargar un VHD Linux tooAzure | Documentos de Microsoft
description: "Crear y cargar un Azure disco duro virtual (VHD) que contiene el sistema de operativo Linux Hola con modelo de implementación clásica de Hola"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a>Crear y cargar un disco duro Virtual que contiene Hola sistema operativo Linux
> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. También puede [cargar una imagen de disco personalizada mediante Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Este artículo muestra cómo toocreate y cargar un disco duro virtual (VHD), por lo que puede usar como su propia imagen toocreate las máquinas virtuales en Azure. Obtenga información acerca de cómo tooprepare sistema de operativo Hola por lo que puede usar toocreate varias máquinas virtuales basado en dicha imagen. 


## <a name="prerequisites"></a>Requisitos previos
Este artículo se supone que dispone de hello siguientes elementos:

* **Sistema operativo Linux instalado en un archivo .vhd** -ha instalado un [distribución de Linux están aprobados Azure](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (o consulte [información para las distribuciones no aprobadas](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa de disco virtual en formato de disco duro virtual de Hola. Varias herramientas existen toocreate una máquina virtual y el disco duro virtual:
  * Instalar y configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), teniendo cuidado de toouse del disco duro virtual como el formato de imagen. Si es necesario, puede [convertir una imagen](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) con `qemu-img convert`.
  * También puede usar Hyper-V [en Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [en Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> no se admite el formato VHDX más reciente de Hello en Azure. Cuando se crea una máquina virtual, especifique VHD como formato de Hola. Si es necesario, se puede convertir VHDX discos tooVHD con [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet de PowerShell. Además, Azure no permite cargar discos duros virtuales dinámicos, por lo que necesita tooconvert tal toostatic discos VHD antes de cargar. Puede usar herramientas como [utilidades de disco duro virtual de Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert discos dinámicos durante el proceso de Hola de carga tooAzure.

* **Interfaz de línea de comandos de Azure** -Hola de instalación más reciente [interfaz de línea de comandos de Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) hello tooupload disco duro virtual.

<a id="prepimage"></a>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a>Paso 1: Preparar Hola imagen toobe cargado
Azure admite varias distribuciones Linux (consulte [Distribuciones aprobadas](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Hola siguientes artículos le guiarán por cómo tooprepare Hola diversas distribuciones de Linux que se admiten en Azure. Después de completar los pasos de Hola Hola siguiendo a guías, proceder vuelve aquí una vez que tenga un archivo de disco duro virtual que está listo tooupload tooAzure:

* **[Distribuciones basadas en CentOS](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES y openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Otras distribuciones no aprobadas](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

> [!NOTE]
> Hola SLA de la plataforma Windows Azure aplica máquinas toovirtual ejecuta Hola se utiliza sistema operativo solo cuando uno de hello están aprobados distribuciones de Linux con detalles de configuración de hello tal como se especifica en 'Admite versiones' en [Azure-Endorsed distribuciones Linux en ](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Todas las distribuciones de Linux en la Galería de imágenes de Azure Hola son refrendadas distribuciones con la configuración necesaria de Hola.
> 
> 

Consulte también hello  **[notas sobre la instalación de Linux](../create-upload-generic.md#general-linux-installation-notes)**  para obtener más sugerencias sobre cómo preparar imágenes de Linux de Azure.

<a id="connect"></a>

## <a name="step-2-prepare-hello-connection-tooazure"></a>Paso 2: Preparar Hola conexión tooAzure
Asegúrese de que se usa Hola CLI de Azure en el modelo de implementación clásica de hello (`azure config mode asm`), a continuación, inicie sesión en la cuenta de tooyour:

```azurecli
azure login
```


<a id="upload"></a>

## <a name="step-3-upload-hello-image-tooazure"></a>Paso 3: Cargar Hola imagen tooAzure
Necesita el archivo de disco duro virtual para una tooupload de cuenta de almacenamiento. Puede seleccionar una cuenta de almacenamiento existente o [crear una nueva](../../../storage/common/storage-create-storage-account.md).

Utilizar imagen de hello Azure CLI tooupload hello mediante Hola siguiente comando:

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

En el ejemplo de Hola anterior:

* **BlobStorageURL** es dirección URL de Hola Hola cuenta de almacenamiento tiene previsto toouse
* **YourImagesFolder** esté contenedor Hola dentro del almacenamiento de blobs donde desee toostore las imágenes
* **VHDName** es Hola etiqueta que aparece en el portal tooidentify Hola disco duro.
* **PathToVHDFile** es la ruta de acceso completa de Hola y el nombre de archivo .vhd de hello en su equipo.

Hola siguiente comando muestra un ejemplo completo:

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a>Paso 4: Crear una máquina virtual desde la imagen de Hola
Crear una VM con `azure vm create` Hola igual que una máquina virtual regular. Especificar nombre de Hola se le asignó la imagen en el paso anterior de Hola. En el siguiente ejemplo de Hola, usamos hello **myImage** nombre de la imagen en el paso anterior de Hola:

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

toocreate sus propias máquinas virtuales, proporcionar su propio nombre de usuario + el contraseña, la ubicación, el nombre DNS y el nombre de la imagen.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, consulte [referencia de CLI de Azure para el modelo de implementación clásica Azure hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
