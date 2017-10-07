---
title: "una imagen personalizada de laboratorios de desarrollo y pruebas de Azure desde una máquina virtual aaaCreate | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una imagen personalizada en los laboratorios de desarrollo y pruebas de Azure desde una VM aprovisionado con Hola portal de Azure"
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
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a>Crear una imagen personalizada a partir de una máquina virtual

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a>Instrucciones paso a paso

Puede crear una imagen personalizada de una máquina virtual con aprovisionamiento y después usar esa imagen personalizada toocreate máquinas virtuales idénticas. Hola siguientes pasos muestra cómo toocreate personalizado de la imagen de una máquina virtual:

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.

1. En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.  

1. En la hoja del laboratorio de hello, seleccione **mis equipos virtuales**.
 
1. En hello **mis equipos virtuales** hoja, VM Hola seleccione del que desea que la imagen personalizada de toocreate Hola.

1. En la hoja de la máquina virtual de hello, seleccione **crear imagen personalizada (VHD)**.

    ![Crear elemento de menú de imagen personalizada](./media/devtest-lab-create-template/create-custom-image.png)

1. En hello **crear imagen** hoja, escriba un nombre y una descripción para la imagen personalizada. Esta información se muestra en la lista de Hola de bases de cuando se crea una máquina virtual.

    ![Crear imagen personalizada](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. Seleccione si se ejecutó sysprep en hello máquina virtual. Si no se ha ejecutado sysprep hello en hello VM, especifique si desea ejecutar cuando se crea una máquina virtual desde su imagen personalizada de sysprep.

1. Seleccione **Aceptar** cuando toocreate terminado Hola imagen personalizada.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Entradas blogs relacionadas

- [Custom images or formulas? (¿Imágenes personalizadas o fórmulas?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Copying Custom Images between Azure DevTest Labs (Copiar imágenes personalizadas entre instancias de Azure DevTest Labs)](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Pasos siguientes

- [Agregar un laboratorio de tooyour VM](./devtest-lab-add-vm-with-artifacts.md)
