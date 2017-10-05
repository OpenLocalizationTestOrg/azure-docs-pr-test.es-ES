---
title: "Visualización y uso de una plantilla de Azure Resource Manager en una máquina virtual | Microsoft Docs"
description: "Aprenda a usar la plantilla de Azure Resource Manager desde una máquina virtual para crear otras máquinas virtuales"
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
ms.openlocfilehash: 12cdb61667f77215c894800d5c439235e767a26b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-a-virtual-machines-azure-resource-manager-template"></a>Uso de una plantilla de Azure Resource Manager con una máquina virtual

Al crear una máquina virtual (VM) en DevTest Labs a través de [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), puede ver la plantilla de Azure Resource Manager antes de guardar la máquina virtual. La plantilla, a continuación, se puede usar como punto de partida para crear más máquinas virtuales de laboratorio con la misma configuración.

Este artículo describe cómo ver la plantilla de Resource Manager al crear una máquina virtual y cómo implementarla posteriormente para automatizar la creación de la misma máquina virtual.

## <a name="multi-vm-vs-single-vm-resource-manager-templates"></a>Plantillas de Resource Manager de una sola máquina virtual o de varias
Hay dos maneras de crear máquinas virtuales en DevTest Labs mediante una plantilla de Resource Manager: aprovisionar el recurso Microsoft.DevTestLab/labs/virtualmachines o el recurso Microsoft.Commpute/virtualmachines. Cada una se utiliza en escenarios diferentes y requiere permisos distintos.

- Las plantillas de Resource Manager que usan un tipo de recurso Microsoft.DevTestLab/labs/virtualmachines (tal y como se declara en la propiedad "resource" en la plantilla) pueden aprovisionar máquinas virtuales de laboratorio individuales. Cada máquina virtual aparecerá entonces como un único elemento en la lista de máquinas virtuales de DevTest Labs:

   ![Enumeración de máquinas virtuales como elementos únicos en la lista de máquinas virtuales de DevTest Labs](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-item.png)

   Este tipo de plantilla de Resource Manager se puede aprovisionar a través del comando de Azure PowerShell **New-AzureRmResourceGroupDeployment** o mediante el comando de la CLI de Azure **az group deployment create**. Se necesitan permisos de administrador, por lo que los usuarios asignados a un rol de usuario de DevTest Labs no pueden realizar la implementación. 

- Las plantillas de Resource Manager que usan un tipo de recurso Microsoft.Compute/virtualmachines pueden aprovisionar varias máquinas virtuales como un único entorno en la lista de máquinas virtuales de DevTest Labs:

   ![Enumeración de máquinas virtuales como elementos únicos en la lista de máquinas virtuales de DevTest Labs](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-environment.png)

   Las máquinas virtuales en el mismo entorno pueden administrarse conjuntamente y compartir el mismo ciclo de vida. Los usuarios asignados a un rol de usuario de DevTest Labs pueden crear entornos con esas plantillas, siempre y cuando el administrador haya configurado el laboratorio de ese modo.

El resto de este artículo describe las plantillas de Resource Manager que utilizan Mirosoft.DevTestLab/labs/virtualmachines. Los administradores de DevTest Labs las usan para automatizar la creación de máquinas virtuales de laboratorio (por ejemplo, las VM reclamables) o la generación de imágenes maestras (por ejemplo, la factoría de imágenes).

En [Procedimientos recomendados para crear plantillas de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) se ofrecen muchas directrices y sugerencias para ayudarle a crear plantillas de Azure Resource Manager confiables y fáciles de usar.

## <a name="view-and-save-a-virtual-machines-resource-manager-template"></a>Visualización y guardado de una plantilla de Resource Manager de una máquina virtual
1. Siga los pasos de [Creación de su primera máquina virtual en un laboratorio](devtest-lab-create-first-vm.md) para empezar a crear una máquina virtual.
1. Escriba la información necesaria para la máquina virtual y agréguele cualquier artefacto que desee.
1. En la parte inferior de la ventana Parámetros de configuración, elija **View ARM template** (Ver plantilla ARM).

   ![Botón View ARM template (Ver plantilla ARM)](./media/devtest-lab-use-arm-template/devtestlab-lab-view-rm-template.png)
1. Copie y guarde la plantilla de Resource Manager para usarla más adelante para crear otra máquina virtual.

   ![Plantilla de Resource Manager que guardar para usarla más adelante](./media/devtest-lab-use-arm-template/devtestlab-lab-copy-rm-template.png)

Después de guardar la plantilla de Resource Manager, debe actualizar la sección de parámetros de la plantilla para poder utilizarla. Puede crear un archivo parameter.json que personalice solamente los parámetros, fuera de la plantilla de Resource Manager real. 

![Personalización de parámetros con un archivo JSON](./media/devtest-lab-use-arm-template/devtestlab-lab-custom-params.png)

## <a name="deploy-a-resource-manager-template-to-create-a-vm"></a>Implementación de una plantilla de Resource Manager para crear una máquina virtual
Después de guardar una plantilla de Resource Manager y personalizarla según sus necesidades, puede utilizarla para automatizar la creación de una máquina virtual. En [Implementación de recursos con plantillas de Resource Manager y Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) se describe cómo usar PowerShell de Azure con plantillas de Resource Manager para implementar recursos en Azure. En [Implementación de recursos con plantillas de Resource Manager y CLI de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli) se describe cómo usar CLI de Azure con plantillas de Resource Manager para implementar recursos en Azure.

> [!NOTE]
> Solo un usuario con permisos de propietario de laboratorio puede crear máquinas virtuales desde una plantilla de Resource Manager con Azure PowerShell. Si desea automatizar la creación de máquinas virtuales mediante una plantilla de Resource Manager y solo tiene permisos de usuario, puede usar el comando [ **az lab vm create** de la CLI ](https://docs.microsoft.com/cli/azure/lab/vm#create).

### <a name="next-steps"></a>Pasos siguientes
* Aprenda a [crear entornos de varias máquinas virtuales con plantillas de Resource Manager](devtest-lab-create-environment-from-arm.md).
* Explore más plantillas Resource Manager de inicio rápido para la automatización de DevTest Labs desde el [repositorio público de GitHub de DevTest Labs](https://github.com/Azure/azure-quickstart-templates).
