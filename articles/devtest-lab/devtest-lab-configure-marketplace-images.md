---
title: "configuración de la imagen aaaConfigure Azure Marketplace en los laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft"
description: "Configuración de las imágenes de Azure Marketplace que se pueden usar al crear una máquina virtual en Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a>Configuración de imágenes de Azure Marketplace en Azure DevTest Labs
Laboratorios de desarrollo y pruebas admite crear máquinas virtuales basadas en imágenes de Azure Marketplace dependiendo de cómo se haya configurado Azure Marketplace imágenes toobe utilizado en el laboratorio. Este artículo muestra cómo toospecify que, si lo hay, imágenes de Azure Marketplace se pueden usar al crear máquinas virtuales en un laboratorio. Esto garantiza que el equipo sólo tiene imágenes de Marketplace de toohello de acceso que necesitan. 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a>Elección de las imágenes de Azure Marketplace que se permiten al crear una máquina virtual
1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.
3. En lista de Hola de laboratorios, seleccione laboratorio deseado Hola. 
4. En la hoja del laboratorio de hello, seleccione **directivas y configuración**.
5. En la hoja **Configuration and policies** (Directivas y configuración) de **Virtual Machine Bases** (Bases de datos de las máquinas virtuales), seleccione **Marketplace images** (Imágenes de Marketplace).
6. Especifique si desea que todos los Hola toobe de imágenes de Azure Marketplace completo disponible para su uso como base de una nueva máquina virtual. Si selecciona **Sí**, a continuación, todos los hello Azure Marketplace que cumplan Hola a todos los siguientes criterios se permiten imágenes en laboratorio hello:
   
   * imagen de Hello crea una sola máquina virtual, **y**
   * imagen de Hello usa las máquinas virtuales de Azure Resource Manager tooprovision, **y**
   * imagen de Hello no requiere la compra de un plan de licencias adicionales
     
    Si no desea que ningún toobe de imágenes permite, o si desea toospecify qué imágenes se pueden usar, seleccione **No**.
     
     ![Opción tooallow toobe de imágenes de Marketplace todos los utiliza como imágenes de base para las máquinas virtuales](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. Si selecciona **No** toohello anterior paso a paso, hello **permitido imágenes o seleccionar todo** casilla de verificación está habilitada. 
   Puede usar esta opción junto con el cuadro de búsqueda, hello tooquickly seleccione o anule la selección de todos los elementos de hello aparece en la lista de Hola.
   * Seleccione hello Azure Marketplace imágenes que desee tooallow creación de máquinas virtuales individualmente activando la casilla de verificación correspondiente de la imagen.
   * No se selecciona nada en lista de hello si no desea tooallow cualquier toobe de imágenes de Azure Marketplace utilizado en el laboratorio de Hola.
   
    ![Puede especificar qué imágenes de Azure Marketplace se pueden usar como imágenes base para las máquinas virtuales](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Pasos siguientes
Una vez haya configurado el modo en que se permiten imágenes de Azure Marketplace al crear una máquina virtual, paso siguiente hello es demasiado[agregar un laboratorio VM tooyour](devtest-lab-add-vm-with-artifacts.md).

