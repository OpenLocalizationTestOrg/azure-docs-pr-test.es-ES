---
title: aaaCreate una imagen personalizada de laboratorios de desarrollo y pruebas de Azure desde un archivo VHD | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una imagen personalizada en los laboratorios de desarrollo y pruebas de Azure desde un archivo de disco duro virtual mediante Hola portal de Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a>Crear una imagen personalizada a partir de un archivo VHD

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>Instrucciones paso a paso

Hello pasos siguientes le guían por la creación de una imagen personalizada desde un archivo de disco duro virtual mediante Hola portal de Azure:

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.

1. En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.  

1. En la hoja del laboratorio de hello, seleccione **configuración**. 

1. En el laboratorio de hello **configuración** hoja, seleccione **imágenes personalizadas (VHD)**.

1. En hello **imágenes personalizadas** hoja, seleccione **+ agregar**.

    ![Adición de imágenes personalizadas](./media/devtest-lab-create-template/add-custom-image.png)

1. Escriba el nombre de Hola de imagen personalizada de Hola. Este nombre se muestra en la lista de Hola de imágenes de base al crear una máquina virtual.

1. Escriba la descripción de Hola de imagen personalizada de Hola. Esta descripción se muestra en la lista de Hola de imágenes de base al crear una máquina virtual.

1. Seleccione **VHD**.

1. De hello **VHD** hoja, archivo de disco duro virtual de hello seleccione deseado.

1. Seleccione **Aceptar** tooclose hello **VHD** hoja.

1. Seleccione la **configuración del sistema operativo**.

1. En hello **configuración del sistema operativo** ficha, seleccione **Windows** o **Linux**.

1. Si **Windows** está seleccionada, especifique a través de la casilla de verificación de hello si *Sysprep* se ha ejecutado en la máquina de Hola. 

1. Seleccione **Aceptar** tooclose hello **configuración del sistema operativo** hoja.

1. Seleccione **Aceptar** imagen personalizada de toocreate Hola.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Entradas blogs relacionadas

- [Custom images or formulas? (¿Imágenes personalizadas o fórmulas?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Copying Custom Images between Azure DevTest Labs (Copiar imágenes personalizadas entre instancias de Azure DevTest Labs)](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Pasos siguientes

- [Agregar un laboratorio de tooyour VM](./devtest-lab-add-vm-with-artifacts.md)
