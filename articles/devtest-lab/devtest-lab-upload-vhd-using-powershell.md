---
title: aaaUpload VHD archivo laboratorios de desarrollo y pruebas de tooAzure mediante PowerShell | Documentos de Microsoft
description: Cargar la cuenta de almacenamiento del toolab del archivo de disco duro virtual con PowerShell
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a>Cargar la cuenta de almacenamiento del toolab del archivo de disco duro virtual con PowerShell

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

En los laboratorios de desarrollo y pruebas de Azure, archivos de disco duro virtual pueden ser toocreate usa imágenes personalizadas, que son máquinas virtuales de tooprovision usado. Hello pasos siguientes le guían a través mediante PowerShell tooupload cuenta de almacenamiento del laboratorio tooa de archivo de disco duro virtual. Una vez que haya cargado el archivo VHD, Hola [pasos siguientes sección](#next-steps) enumera algunos artículos que ilustran cómo toocreate una imagen personalizada de hello carga archivo de disco duro virtual. Para más información sobre discos y discos duros virtuales en Azure, consulte [Acerca de los discos y los discos duros virtuales para máquinas virtuales](../virtual-machines/linux/about-disks-and-vhds.md).

## <a name="step-by-step-instructions"></a>Instrucciones paso a paso

Hola siguientes pasos le indican recorrido a través de la carga de un disco duro virtual archivo laboratorios de desarrollo y pruebas de tooAzure mediante PowerShell. 

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.

1. En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.  

1. En la hoja del laboratorio de hello, seleccione **configuración**. 

1. En el laboratorio de hello **configuración** hoja, seleccione **imágenes personalizadas (VHD)**.

1. En hello **imágenes personalizadas** hoja, seleccione **+ agregar**. 

1. En hello **imagen personalizada** hoja, seleccione **VHD**.

1. En hello **VHD** hoja, seleccione **cargar un VHD con PowerShell**.

    ![Carga del VHD mediante PowerShell](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. En hello **cargar una imagen con PowerShell** hoja, editor de texto de tooa de secuencia de comandos PowerShell de hello generado de copia.

1. Modificar hello **LocalFilePath** parámetro de hello **Add-AzureVhd** cmdlet toopoint toohello ubicación del archivo de disco duro virtual que desee tooupload Hola.

1. En un símbolo del sistema de PowerShell, ejecute hello **Add-AzureVhd** cmdlet (con hello modificado **LocalFilePath** parámetro).

> [!WARNING] 
> 
> proceso de Hola de cargar un archivo de disco duro virtual puede ser larga según el tamaño de hello del archivo de disco duro virtual de hello y la velocidad de conexión.

## <a name="next-steps"></a>Pasos siguientes

- [Crear una imagen personalizada en los laboratorios de desarrollo y pruebas de Azure desde un archivo de disco duro virtual mediante Hola portal de Azure](devtest-lab-create-template.md)
- [Creación de una imagen personalizada en Azure DevTest Labs a partir de un archivo VHD mediante PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
