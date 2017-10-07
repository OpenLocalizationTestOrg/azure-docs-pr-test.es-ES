---
title: "aaaCreate la primera VM en un laboratorio de prácticas de desarrollo y pruebas de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate la primera máquina virtual en un laboratorio de prácticas de desarrollo y pruebas de Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a>Create your first VM in a lab in Azure DevTest Labs (Creación de su primera máquina virtual en un laboratorio en Azure DevTest Labs)

Cuando inicialmente tener acceso a los laboratorios de desarrollo y pruebas y desea toocreate la primera máquina virtual, es probable que lo hará con cargado previamente [imagen de marketplace base](devtest-lab-configure-marketplace-images.md). Más adelante podrá también pueden toochoose desde una [imagen personalizada y una fórmula](devtest-lab-add-vm.md) al crear más máquinas virtuales. 

Este tutorial le guiará a través de hello tooadd portal Azure su primera práctica tooa VM en los laboratorios de desarrollo y pruebas.

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a>Los pasos tooadd su primera práctica tooa VM en los laboratorios de desarrollo y pruebas de Azure
1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.
1. En lista de Hola de laboratorios, seleccione laboratorio hello en el que desea toocreate Hola máquina virtual.  
1. En el laboratorio de hello **Introducción** hoja, seleccione **+ agregar**.  

    ![Botón Agregar VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. En hello **elegir una base de** hoja, seleccione la imagen de un mercado para hello máquina virtual.
1. En hello **Máquina Virtual** hoja, escriba un nombre para la nueva máquina virtual de Hola Hola **nombre de máquina Virtual** cuadro de texto.

    ![Hoja de la máquina virtual de laboratorio](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. Escriba un **nombre de usuario** que se conceden privilegios de administrador en la máquina virtual de Hola.  
1. Especifique una contraseña en el campo de texto hello texto **escriba un valor**.
1. Hola **tipo de disco de máquina Virtual** determina qué tipo de disco de almacenamiento está permitida para las máquinas virtuales de hello en laboratorio Hola.
1. Seleccione **tamaño de máquina Virtual** y seleccione una de hello predefinidos elementos que especifiquen los núcleos de procesador de hello, el tamaño de RAM y tamaño de unidad de disco duro de Hola de hello toocreate de máquina virtual.
1. Seleccione **artefactos** y - Hola seleccione en lista de artefactos - y configurar los artefactos de Hola que desea que la imagen base de tooadd toohello.
    **Nota:** si nuevos laboratorios de tooDevTest o configuración de artefactos, consulte toohello [agregar un tooa artefacto existente VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sección y, a continuación, regrese aquí cuando termine.
1. Seleccione **crear** tooadd Hola especificado laboratorio toohello de máquina virtual.

   hoja de laboratorio Hello muestra el estado de Hola de creación de la máquina virtual de hello - primero como **crear**, a continuación, como **ejecutando** después de hello máquina virtual se ha iniciado.

## <a name="next-steps"></a>Pasos siguientes
* Una vez Hola se ha creado la máquina virtual, puede conectarse toohello VM seleccionando **conectar** en la hoja de la máquina virtual de Hola.
* Extraer del repositorio [agregar un laboratorio VM tooa](devtest-lab-add-vm.md) para obtener información más completa acerca de cómo agregar máquinas virtuales posteriores en el laboratorio.
* Explorar hello [Galería de plantillas de desarrollo y pruebas laboratorios Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).
