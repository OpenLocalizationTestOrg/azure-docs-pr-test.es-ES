---
title: aaaDownload un VHD de Windows de Azure | Documentos de Microsoft
description: Descargar un disco duro virtual de Windows con hello portal de Azure.
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
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a>Descargar un VHD de Windows desde Azure

En este artículo, aprenderá cómo toodownload una [disco duro virtual (VHD) de Windows](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) archivo utilizasen Azure Hola portal de Azure. 

Máquinas virtuales (VM) en uso Azure [discos](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) como un toostore lugar un sistema operativo, aplicaciones y datos. Todas las máquinas virtuales de Azure tienen al menos dos discos: un disco de sistema operativo Windows y un disco temporal. disco del sistema operativo Hola se crea inicialmente desde una imagen, y el disco del sistema operativo de Hola y de imagen de Hola son discos duros virtuales almacenados en una cuenta de almacenamiento de Azure. Las máquinas virtuales también pueden tener uno o más discos de datos que también se almacenan en discos duros virtuales.

## <a name="stop-hello-vm"></a>Detener Hola VM

No se puede descargar un disco duro virtual de Azure si se adjunta tooa ejecutando la máquina virtual. Debe toodownload VM de hello toostop un disco duro virtual. Si desea toouse un VHD como un [imagen](tutorial-custom-images.md) toocreate otras máquinas virtuales con discos nuevos, use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize Hola sistema operativo contenido en el archivo hello y, a continuación, detener Hola máquina virtual. Hola toouse VHD como un disco para una nueva instancia de una máquina virtual existente o un disco de datos, solo necesita toostop y cancelar la asignación de hello máquina virtual.

toouse Hola VHD como una imagen toocreate otras máquinas virtuales, siga estos pasos:

1.  Si aún no lo ha hecho, inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2.  [Conectar toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
3.  En hello VM, abra la ventana de símbolo de hello como administrador.
4.  Cambie el directorio de hello demasiado*%windir%\system32\sysprep* y ejecute sysprep.exe.
5.  En el cuadro de diálogo de la herramienta de preparación del sistema de hello, seleccione **sistema Out-of-Box experiencia inmediata (OOBE)**y asegúrese de que **generalizar** está seleccionada.
6.  En Opciones de apagado, seleccione **Apagar** y luego haga clic en **Aceptar**. 

Hola toouse VHD como un disco para una nueva instancia de una máquina virtual existente o un disco de datos, siga estos pasos:

1.  En el menú del concentrador Hola Hola portal de Azure, haga clic en **máquinas virtuales**.
2.  Seleccione Hola VM de hello lista.
3.  En la hoja de Hola para hello VM, haga clic en **detener**.

    ![Detención de la máquina virtual](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>Generación de dirección URL de SAS

archivo de disco duro virtual de hello toodownload, deberá toogenerate un [firma de acceso compartido (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) dirección URL. Cuando se genera la dirección URL de hello, una fecha de caducidad se asigna toohello URL.

1.  En el menú de Hola de hoja de Hola para hello VM, haga clic en **discos**.
2.  Seleccionar disco de sistema operativo de Hola para hello VM y, a continuación, haga clic en **exportar**.
3.  Establecer tiempo de expiración de Hola de dirección URL de hello demasiado*36000*.
4.  Haga clic en **Generar dirección URL**.

    ![Generar dirección URL](./media/download-vhd/export-generate.png)

> [!NOTE]
> hora de expiración de Hello ha aumentado de hello predeterminado tooprovide suficiente tiempo toodownload Hola archivo VHD grande para un sistema operativo Windows Server. Puede esperar a que un archivo de disco duro virtual que contenga tootake de sistema operativo de Windows Server de hello toodownload de varias horas dependiendo de la conexión. Si va a descargar un disco duro virtual para un disco de datos, el tiempo predeterminado de hello es suficiente. 
> 
> 

## <a name="download-vhd"></a>Descargar VHD

1.  En dirección URL de Hola que generó, haga clic en archivo de disco duro virtual de hello de descarga.

    ![Descargar VHD](./media/download-vhd/export-download.png)

2.  Puede que necesite tooclick **guardar** en descarga de hello explorador toostart Hola. nombre predeterminado de Hello para el archivo de disco duro virtual de hello es *abcd*.

    ![Haga clic en Guardar en el Explorador de Hola](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Pasos siguientes

- Obtenga información acerca de cómo demasiado[cargar un tooAzure del archivo de disco duro virtual](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
- [Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Creación de discos administrados a partir de discos no administrados en una cuenta de almacenamiento).
- [Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Administrar discos de Azure con PowerShell).

