---
title: aaaAdd un laboratorio de tooa claimable de VM en los laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooadd un laboratorio de tooa claimable máquina virtual en los laboratorios de desarrollo y pruebas de Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: fe6385ae2e59b9636b82aec250dc3a1f8a40ba5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>Agregar un laboratorio de tooa claimable de VM en los laboratorios de desarrollo y pruebas de Azure
Agregar un laboratorio de tooa claimable de máquina virtual en un toohow de manera similar [agregar una máquina virtual estándar](devtest-lab-add-vm.md) : en un *base* decir cualquiera una [imagen personalizada](devtest-lab-create-template.md), [fórmula](devtest-lab-manage-formulas.md), o [imagen de Marketplace](devtest-lab-configure-marketplace-images.md). Este tutorial le guía a través mediante hello Azure tooadd portal un laboratorio de tooa claimable de VM en los laboratorios de desarrollo y pruebas y se muestra el proceso de Hola que Hola tooclaim VM sigue a un usuario.

> [!NOTE]
> Si implementa máquinas virtuales de laboratorio a través de [plantillas de Azure Resource Manager](devtest-lab-create-environment-from-arm.md), puede crear máquinas virtuales claimable establecer hello **allowClaim** tootrue de propiedad en la sección de propiedades de Hola.
>
>

## <a name="steps-tooadd-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>Pasos tooadd un laboratorio de tooa claimable de VM en los laboratorios de desarrollo y pruebas de Azure
1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.
1. En lista de Hola de laboratorios, seleccione laboratorio hello en que desea toocreate Hola VM claimable.  
1. En el laboratorio de hello **Introducción** hoja, seleccione **+ agregar**.  

    ![Botón Agregar VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. En hello **elegir una base de** hoja, seleccione una base de VM de Hola.
1. En hello **Máquina Virtual** hoja, escriba un nombre para la nueva máquina virtual de Hola Hola **nombre de máquina Virtual** cuadro de texto.

    ![Hoja de la máquina virtual de laboratorio](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. Escriba un **nombre de usuario** que se conceden privilegios de administrador en la máquina virtual de Hola.  
1. Si desea que toouse una contraseña almacenados en su [almacén secreto](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), seleccione **usa un secreto guardado**y especifique un valor de clave que corresponde tooyour secreto (contraseña). En caso contrario, especifique una contraseña en el campo de texto hello texto **escriba un valor**.
1. Hola **tipo de disco de máquina Virtual** determina qué tipo de disco de almacenamiento está permitida para las máquinas virtuales de hello en laboratorio Hola.
1. Seleccione **tamaño de máquina Virtual** y seleccione una de hello predefinidos elementos que especifiquen los núcleos de procesador de hello, el tamaño de RAM y tamaño de unidad de disco duro de Hola de hello toocreate de máquina virtual.
1. Seleccione **artefactos** y Hola seleccione en lista de artefactos y configurar los artefactos de Hola que desea que la imagen base de tooadd toohello. Si los nuevos laboratorios de tooDevTest o configuración de artefactos, consulte toohello [agregar un tooa artefacto existente VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sección y, a continuación, regrese aquí cuando termine.
1. Seleccione **configuración avanzada** tooconfigure Hola VM opciones y expiración de las opciones de red. En **opciones de notificación**, elija **Sí** máquina de hello toomake claimable.

  ![Elija toomake Hola VM claimable.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. Si desea tooview o Copiar plantilla de hello Azure Resource Manager, consulte toohello [guardar Azure Resource Manager plantilla](devtest-lab-add-vm.md#save-azure-resource-manager-template) sección y regrese aquí cuando termine.
1. Seleccione **crear** tooadd Hola especificado laboratorio toohello de máquina virtual.
1. hoja de laboratorio Hello muestra el estado de Hola de creación de la máquina virtual de hello - primero como **crear**, a continuación, como **ejecutando** después de hello máquina virtual se ha iniciado.


## <a name="using-a-claimable-vm"></a>Uso de una máquina virtual reclamable

Un usuario puede reclamar cualquier máquina virtual de la lista de Hola de "Máquinas virtuales Claimable", realice uno de estos pasos:

* En la lista Hola de "Máquinas virtuales Claimable" final Hola de hoja de información general del laboratorio de hello, haga doble clic en uno de hello las máquinas virtuales en la lista de Hola y elija **máquina notificación**.

 ![Solicite una máquina virtual reclamable específica.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* En parte superior de Hola de hello **información general sobre** hoja, elija **cualquier notificación**. Una máquina virtual aleatoria se asigna desde la lista de Hola de máquinas virtuales claimable.

 ![Solicite cualquier máquina virtual reclamable.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


Una vez que un usuario reclama una máquina virtual, se mueve a su lista de máquinas virtuales y ya no podrá reclamarla otro usuario.

## <a name="next-steps"></a>Pasos siguientes
* Una vez Hola se ha creado la máquina virtual, puede conectarse toohello VM seleccionando **conectar** en la hoja de la máquina virtual de Hola.
* Explorar hello [Galería de plantillas de desarrollo y pruebas laboratorios Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)
