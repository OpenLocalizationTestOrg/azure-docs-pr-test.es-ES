---
title: aaaAdd un laboratorio de tooa VM en los laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooadd un laboratorio de tooa de máquina virtual en los laboratorios de desarrollo y pruebas de Azure"
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
ms.date: 02/24/2017
ms.author: tarcher
ms.openlocfilehash: 82838e4349550db56de311264c188140b9556b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-vm-tooa-lab-in-azure-devtest-labs"></a>Agregar un laboratorio de tooa VM en los laboratorios de desarrollo y pruebas de Azure
Si ya ha [creado su primera máquina virtual](devtest-lab-create-first-vm.md), es probable que lo hiciera desde una [imagen de Marketplace](devtest-lab-configure-marketplace-images.md) precargada. Ahora, si desea tooadd posteriores máquinas virtuales tooyour laboratorio, también puede elegir un *base* decir ya sea un [imagen personalizada](devtest-lab-create-template.md) o un [fórmula](devtest-lab-manage-formulas.md). Este tutorial le guía a través mediante hello tooadd portal Azure un laboratorio de tooa VM en los laboratorios de desarrollo y pruebas.

Este artículo también muestra cómo toomanage Hola artefactos para una máquina virtual en el laboratorio.

## <a name="steps-tooadd-a-vm-tooa-lab-in-azure-devtest-labs"></a>Pasos tooadd un laboratorio de tooa VM en los laboratorios de desarrollo y pruebas de Azure
1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.
1. En lista de Hola de laboratorios, seleccione laboratorio hello en el que desea toocreate Hola máquina virtual.  
1. En el laboratorio de hello **Introducción** hoja, seleccione **+ agregar**.  

    ![Botón Agregar VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. En hello **elegir una base de** hoja, seleccione una base de VM de Hola.
1. En hello **Máquina Virtual** hoja, escriba un nombre para la nueva máquina virtual de Hola Hola **nombre de máquina Virtual** cuadro de texto.

    ![Hoja de la máquina virtual de laboratorio](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. Escriba un **nombre de usuario** que se conceden privilegios de administrador en la máquina virtual de Hola.  
1. Si desea que toouse una contraseña almacenados en su [almacén secreto](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), seleccione **usa un secreto guardado**y especifique un valor de clave que corresponde tooyour secreto (contraseña). En caso contrario, especifique una contraseña en el campo de texto hello texto **escriba un valor**.
1. Hola **tipo de disco de máquina Virtual** determina qué tipo de disco de almacenamiento está permitida para las máquinas virtuales de hello en laboratorio Hola.
1. Seleccione **tamaño de máquina Virtual** y seleccione una de hello predefinidos elementos que especifiquen los núcleos de procesador de hello, el tamaño de RAM y tamaño de unidad de disco duro de Hola de hello toocreate de máquina virtual.
1. Seleccione **artefactos** y - Hola seleccione en lista de artefactos - y configurar los artefactos de Hola que desea que la imagen base de tooadd toohello.
    **Nota:** si nuevos laboratorios de tooDevTest o configuración de artefactos, consulte toohello [agregar un tooa artefacto existente VM](#add-an-existing-artifact-to-a-vm) sección y, a continuación, regrese aquí cuando termine.
1. Seleccione **configuración avanzada** tooconfigure Hola VM opciones y expiración de las opciones de red. 

   tooset una opción de caducidad, elija toospecify de icono de calendario Hola una fecha en la que Hola VM se eliminarán automáticamente.  De forma predeterminada, el Hola VM nunca expirará. 
1. Si desea tooview o Copiar plantilla de hello Azure Resource Manager, consulte toohello [guardar Azure Resource Manager plantilla](#save-azure-resource-manager-template) sección y regrese aquí cuando termine.
1. Seleccione **crear** tooadd Hola especificado laboratorio toohello de máquina virtual.
1. hoja de laboratorio Hello muestra el estado de Hola de creación de la máquina virtual de hello - primero como **crear**, a continuación, como **ejecutando** después de hello máquina virtual se ha iniciado.

> [!NOTE]
> [Agregar una máquina virtual claimable](devtest-lab-add-claimable-vm.md) muestra cómo toomake Hola VM claimable para que esté disponible para su uso por cualquier usuario de laboratorio Hola.
>
>

## <a name="add-an-existing-artifact-tooa-vm"></a>Agregar un tooa de artefacto VM existente
Al crear una máquina virtual, puede agregar artefactos existentes. Cada práctica incluye artefactos de hello repositorio público de artefacto de laboratorios de desarrollo y pruebas, así como los artefactos que ha creado y agregado tooyour posee el repositorio de artefactos.

* Laboratorios de desarrollo y pruebas Azure *artefactos* le permiten especificar *acciones* que se realizan cuando se aprovisiona Hola VM, como ejecutar scripts de Windows PowerShell, ejecute comandos de Bash e instalar software.
* Artefacto *parámetros* le permiten personalizar el artefacto de Hola para su escenario concreto

Hola a toodiscover toocreate artefactos, vea el artículo, [Obtenga información acerca de cómo tooauthor sus propios artefactos para usar con laboratorios de desarrollo y pruebas](devtest-lab-artifact-author.md).

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.
1. En lista de Hola de laboratorios, seleccione laboratorio Hola que contiene la máquina virtual de hello con el que desea toowork.  
1. Seleccione **My virtual machines** (Mis máquinas virtuales).
1. Seleccione Hola había deseado de máquina virtual.
1. Seleccione **Artifacts** (Artefactos). 
1. Seleccione **Apply artifacts** (Aplicar artefactos).
1. En hello **aplicar artefactos** hoja, artefacto Hola seleccione desea tooadd toohello máquina virtual.
1. En hello **agregar artefactos** hoja, escriba Hola requerido valores de parámetro y los parámetros opcionales que necesita.  
1. Seleccione **agregar** tooadd Hola artefacto y devuelva toohello **aplicar artefactos** hoja.
1. Siga agregando los artefactos que necesite para la máquina virtual.
1. Una vez que haya agregado los artefactos, también puede [cambiar orden de hello en qué Hola se ejecutan artefactos](#change-the-order-in-which-artifacts-are-run). También puede ir atrás demasiado[ver o modificar un artefacto](#view-or-modify-an-artifact).
1. Cuando haya terminado de agregar artefactos, seleccione **Aplicar**.

## <a name="change-hello-order-in-which-artifacts-are-run"></a>Cambiar el orden de hello en el que se ejecutan los artefactos
De forma predeterminada, las acciones de Hola de artefactos de Hola se ejecutan en orden de hello en el que se agregan toohello máquina virtual. Hello siguientes pasos muestran cómo toochange Hola orden en que Hola se ejecutan los artefactos.

1. En parte superior de Hola de hello **aplicar artefactos** hoja, que indica el número de Hola de artefactos que se han agregado toohello VM de vínculo de hello select.
   
    ![Número de artefactos agregados tooVM](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. En hello **seleccionado artefactos** hoja, arrastrar y colocar artefactos de hello en hello deseado orden. **Nota:** si tiene problemas al arrastrar los artefactos de hello, asegúrese de que va a arrastrar de hello parte izquierda de artefacto de Hola. 
1. Seleccione **Aceptar** cuando haya terminado.  

## <a name="view-or-modify-an-artifact"></a>ver o modificar un artefacto
Hello siguientes pasos muestran cómo tooview o modificar los parámetros de Hola de un artefacto:

1. En parte superior de Hola de hello **aplicar artefactos** hoja, que indica el número de Hola de artefactos que se han agregado toohello VM de vínculo de hello select.
   
    ![Número de artefactos agregados tooVM](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. En hello **seleccionado artefactos** hoja, artefactos de hello select que se desea tooview o editar.  
1. En hello **agregar artefactos** hoja, realice los cambios necesarios y, seleccionen **Aceptar** tooclose hello **agregar artefactos** hoja.
1. Seleccione **Aceptar** tooclose hello **seleccionado artefactos** hoja.

## <a name="save-azure-resource-manager-template"></a>Almacenamiento de una plantilla de Azure Resource Manager
Una plantilla de Azure Resource Manager proporciona una manera declarativa toodefine una implementación repetible. Hola pasos explica cómo toosave Hola plantilla de Azure Resource Manager para hello VM que se está creando.
Una vez guardado, puede usar plantillas de Azure Resource Manager Hola demasiado[implementar nuevas máquinas virtuales con Azure PowerShell](../azure-resource-manager/resource-group-overview.md#template-deployment).

1. En hello **Máquina Virtual** hoja, seleccione **plantilla de ARM de vista**.
2. En hello **plantilla vista Azure Resource Manager** hoja, texto de la plantilla de hello select.
3. Copie toohello Portapapeles de hello texto seleccionado.
4. Seleccione **Aceptar** tooclose hello **hoja de la plantilla de administrador de recursos de Azure de vista**.
5. Abra un editor de texto.
6. Pegar texto de la plantilla de Hola desde el Portapapeles de Hola.
7. Guarde el archivo hello para su uso posterior.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Pasos siguientes
* Una vez Hola se ha creado la máquina virtual, puede conectarse toohello VM seleccionando **conectar** en la hoja de la máquina virtual de Hola.
* Obtenga información acerca de cómo demasiado[crear artefactos personalizados para la máquina virtual de laboratorios de desarrollo y pruebas](devtest-lab-artifact-author.md).
* Explorar hello [Galería de plantillas de desarrollo y pruebas laboratorios Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
