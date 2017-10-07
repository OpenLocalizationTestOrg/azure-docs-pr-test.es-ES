---
title: aaaDownload un VHD de Linux de Azure | Documentos de Microsoft
description: Descargar un VHD de Linux con hello Azure CLI y Hola portal de Azure.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a>Descarga de un VHD de Linux desde Azure

En este artículo, aprenderá cómo toodownload una [disco duro virtual (VHD) de Linux](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Hola de archivo de Azure mediante Azure CLI y portal de Azure. 

Máquinas virtuales (VM) en uso Azure [discos](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) como un toostore lugar un sistema operativo, aplicaciones y datos. Todas las máquinas virtuales de Azure tienen al menos dos discos: un disco de sistema operativo Windows y un disco temporal. disco del sistema operativo Hola se crea inicialmente desde una imagen, y el disco del sistema operativo de Hola y de imagen de Hola son discos duros virtuales almacenados en una cuenta de almacenamiento de Azure. Las máquinas virtuales también pueden tener uno o más discos de datos que también se almacenan en discos duros virtuales.

Si aún no lo ha hecho, instale la [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).

## <a name="stop-hello-vm"></a>Detener Hola VM

No se puede descargar un disco duro virtual de Azure si se adjunta tooa ejecutando la máquina virtual. Debe toodownload VM de hello toostop un disco duro virtual. Si desea toouse un VHD como un [imagen](tutorial-custom-images.md) toocreate otras máquinas virtuales con discos nuevos, necesita toodeprovision y generalizar el sistema de operativo Hola contenido en hello de archivos y detener Hola máquina virtual. Hola toouse VHD como un disco para una nueva instancia de una máquina virtual existente o un disco de datos, solo necesita toostop y cancelar la asignación de hello máquina virtual.

toouse Hola VHD como una imagen toocreate otras máquinas virtuales, siga estos pasos:

1. Utilizar SSH, nombre de la cuenta de hello y dirección IP pública de Hola de hello VM tooconnect tooit y Cancelar. Hola + usuario parámetro también elimina la última cuenta de usuario aprovisionado Hola. Si se conversión credenciales de la cuenta en toohello VM, deje esta + parámetro de usuario. Hello en el ejemplo siguiente se quita Hola último usuario aprovisionado cuenta:

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. Inicie sesión en tooyour Azure cuenta con [inicio de sesión de az](https://docs.microsoft.com/cli/azure/#login).
3. Detener y cancelar la asignación Hola máquina virtual.

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. Generalice Hola máquina virtual. 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

Hola toouse VHD como un disco para una nueva instancia de una máquina virtual existente o un disco de datos, siga estos pasos:

1.  Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2.  En el menú del concentrador hello, haga clic en **máquinas virtuales**.
3.  Seleccione Hola VM de hello lista.
4.  En la hoja de Hola para hello VM, haga clic en **detener**.

    ![Detención de la máquina virtual](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>Generación de dirección URL de SAS

archivo de disco duro virtual de hello toodownload, deberá toogenerate un [firma de acceso compartido (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) dirección URL. Cuando se genera la dirección URL de hello, una fecha de caducidad se asigna toohello URL.

1.  En el menú de Hola de hoja de Hola para hello VM, haga clic en **discos**.
2.  Seleccionar disco de sistema operativo de Hola para hello VM y, a continuación, haga clic en **exportar**.
3.  Haga clic en **Generar dirección URL**.

    ![Generar dirección URL](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a>Descargar VHD

1.  En dirección URL de Hola que generó, haga clic en archivo de disco duro virtual de hello de descarga.

    ![Descargar VHD](./media/download-vhd/export-download.png)

2.  Puede que necesite tooclick **guardar** en descarga de hello explorador toostart Hola. nombre predeterminado de Hello para el archivo de disco duro virtual de hello es *abcd*.

    ![Haga clic en Guardar en el Explorador de Hola](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Pasos siguientes

- Obtenga información acerca de cómo demasiado[cargar y crear una VM Linux desde disco personalizado con hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
- [Administrar discos Azure hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

