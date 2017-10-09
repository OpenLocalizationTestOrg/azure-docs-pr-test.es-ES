---
title: "aaaView y usar Azure Resource Manager plantilla una máquina virtual | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola plantilla del Administrador de recursos de Azure desde una máquina virtual toocreate otras máquinas virtuales"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a759d9ce-655c-4ac6-8834-cb29dd7d30dd
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: tarcher
ms.openlocfilehash: b79f7eb4171793681a0b654e6e72a83191c76bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-virtual-machines-azure-resource-manager-template"></a>Uso de una plantilla de Azure Resource Manager con una máquina virtual

Al crear una máquina virtual (VM) en los laboratorios de desarrollo y pruebas a través de hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), puede ver la plantilla de Azure Resource Manager Hola antes de guardar Hola VM. Hello plantilla, a continuación, se puede usar como un toocreate base más máquinas virtuales de laboratorio con Hola la misma configuración.

Este artículo describe cómo tooview Hola plantilla del Administrador de recursos al crear una máquina virtual y cómo toodeploy lo posterior creación tooautomate de Hola misma máquina virtual.

## <a name="multi-vm-vs-single-vm-resource-manager-templates"></a>Plantillas de Resource Manager de una sola máquina virtual o de varias
Hay dos maneras de máquinas virtuales de toocreate en los laboratorios de desarrollo y pruebas mediante una plantilla de administrador de recursos: aprovisionar recursos de Microsoft.DevTestLab/labs/virtualmachines de Hola o aprovisionar hello Microsoft.Commpute/virtualmachines recursos. Cada una se utiliza en escenarios diferentes y requiere permisos distintos.

- Plantillas de administrador de recursos que usan un tipo de recurso Microsoft.DevTestLab/labs/virtualmachines (tal y como se declara en propiedad de "recurso" hello en plantilla hello) pueden aprovisionar máquinas virtuales del laboratorio individuales. Cada máquina virtual, a continuación, aparecerá como un único elemento de lista de máquinas virtuales de laboratorios de desarrollo y pruebas de hello:

   ![Lista de máquinas virtuales como elementos individuales en la lista de máquinas virtuales de hello laboratorios de desarrollo y pruebas](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-item.png)

   Este tipo de plantilla de administrador de recursos se puede aprovisionar a través de hello comando de PowerShell de Azure **New-AzureRmResourceGroupDeployment** o a través de hello comando de CLI de Azure **Crear implementación de grupo az** . Se necesitan permisos de administrador, por lo que los usuarios asignados a un rol de usuario de laboratorios de desarrollo y pruebas no pueden realizar la implementación de Hola. 

- Plantillas de administrador de recursos que usan un tipo de recurso Microsoft.Compute/virtualmachines pueden aprovisionar varias máquinas virtuales como un único entorno en la lista de máquinas virtuales de laboratorios de desarrollo y pruebas de hello:

   ![Lista de máquinas virtuales como elementos individuales en la lista de máquinas virtuales de hello laboratorios de desarrollo y pruebas](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-environment.png)

   Máquinas virtuales en el mismo entorno puede administrarse conjuntamente de Hola y de recurso compartido de Hola mismo ciclo de vida. Los usuarios asignados a un rol de usuario de laboratorios de desarrollo y pruebas pueden crear entornos con esas plantillas como administrador de hello configuró laboratorio Hola de este modo.

resto de Hola de este artículo describe las plantillas de administrador de recursos que utilizan Mirosoft.DevTestLab/labs/virtualmachines. Se utilizan por la creación de máquinas virtuales de laboratorio administradores tooautomate laboratorio (por ejemplo, VM claimable) o la generación de imagen dorada (por ejemplo, el generador de imágenes).

[Las prácticas recomendadas para la creación de plantillas de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) ofrece muchos toohelp directrices y sugerencias crear plantillas de Azure Resource Manager toouse fácil y confiable.

## <a name="view-and-save-a-virtual-machines-resource-manager-template"></a>Visualización y guardado de una plantilla de Resource Manager de una máquina virtual
1. Siga los pasos de hello en [crear la primera máquina virtual en un laboratorio](devtest-lab-create-first-vm.md) toobegin crear una máquina virtual.
1. Especifique la información de hello necesario para la máquina virtual y agregue cualquier artefacto que desee para esta máquina virtual.
1. Final Hola de hello configurar configuración de la ventana, elija **plantilla de ARM de vista**.

   ![Botón View ARM template (Ver plantilla ARM)](./media/devtest-lab-use-arm-template/devtestlab-lab-view-rm-template.png)
1. Copie y guarde toouse de plantilla del Administrador de recursos de hello toocreate posterior otra máquina virtual.

   ![Toosave de plantilla de administrador de recursos para su uso posterior](./media/devtest-lab-use-arm-template/devtestlab-lab-copy-rm-template.png)

Después de haber guardado la plantilla de administrador de recursos de hello, debe actualizar la sección de parámetros de Hola de plantilla de Hola antes de que se puede usar. Puede crear un parameter.json que personaliza solamente los parámetros de hello, fuera de la plantilla de administrador de recursos reales de Hola. 

![Personalización de parámetros con un archivo JSON](./media/devtest-lab-use-arm-template/devtestlab-lab-custom-params.png)

## <a name="deploy-a-resource-manager-template-toocreate-a-vm"></a>Implementar un toocreate de plantilla de administrador de recursos una máquina virtual
Después de guardar una plantilla de administrador de recursos y personalizados para sus necesidades, puede usarlo tooautomate creación de máquinas virtuales. [Implementar los recursos con plantillas de administrador de recursos y Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) describe cómo toouse PowerShell de Azure con el Administrador de recursos plantillas toodeploy su tooAzure de recursos. [Implementar los recursos con plantillas de administrador de recursos y la CLI de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli) describe cómo toouse CLI de Azure con el Administrador de recursos plantillas toodeploy su tooAzure de recursos.

> [!NOTE]
> Solo un usuario con permisos de propietario de laboratorio puede crear máquinas virtuales desde una plantilla de Resource Manager con Azure PowerShell. Si desea la creación de VM tooautomate mediante una plantilla de administrador de recursos y solo tiene permisos de usuario, puede usar hello [ **crear máquinas virtuales del laboratorio de az** comando hello CLI](https://docs.microsoft.com/cli/azure/lab/vm#create).

### <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[crear entornos de varias VM con plantillas de administrador de recursos](devtest-lab-create-environment-from-arm.md).
* Explorar más plantillas de administrador de recursos de inicio rápido para la automatización de laboratorios de desarrollo y pruebas de hello [repositorio público de GitHub de laboratorios de desarrollo y pruebas](https://github.com/Azure/azure-quickstart-templates).
