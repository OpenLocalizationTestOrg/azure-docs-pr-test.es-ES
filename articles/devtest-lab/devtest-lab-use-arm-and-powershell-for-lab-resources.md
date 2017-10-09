---
title: "aaaCreate o modificar laboratorios automáticamente con plantillas del Administrador de recursos de Azure PowerShell | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse plantillas de administrador de recursos de Azure con PowerShell toocreate o modificar laboratorios automáticamente en un laboratorio de desarrollo y pruebas"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: 29c8bc67caaec17b1f8926dde4e5d9d314b06600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a>Creación o modificación de laboratorios automáticamente con plantillas de Azure Resource Manager y PowerShell

DevTest Labs proporciona muchas plantillas de Azure Resource Manager y los scripts de PowerShell que pueden ayudarle a crear rápida y automáticamente nuevos laboratorios o modificar laboratorios existentes y, a continuación, implementar estos recursos.

En este artículo le guía a través del proceso de Hola de uso de estas plantillas y secuencias de comandos de creación de hello tooautomate, la modificación y la implementación de los laboratorios de. En este artículo también muestra dónde puede encontrar más información acerca de cómo toouse PowerShell tooperform algunas tareas en los laboratorios de desarrollo y pruebas.

## <a name="step-1-gather-your-templates-and-scripts"></a>Paso 1: Recopilación de las plantillas y los scripts
Puede encontrar [plantillas de Azure Resource Manager](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) y [scripts de PowerShell](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) creados previamente en nuestro [repositorio de Github](https://github.com/Azure/azure-devtestlab) público. Úselos como están o personalícelos según sus necesidades y almacénelos en su propio [repositorio Git privado](devtest-lab-add-artifact-repo.md). 

## <a name="step-2-modify-your-azure-resource-manager-template"></a>Paso 2: Edición de la plantilla de Azure Resource Manager
Puede seguir los pasos de hello en [crear la primera plantilla de Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) si nunca ha creado una plantilla de antes.

Además, [las prácticas recomendadas para la creación de plantillas de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) ofrece muchos toohelp directrices y sugerencias crear plantillas de Azure Resource Manager toouse fácil y confiable. Normalmente, utilizará una variación de uno de los enfoques de Hola o ejemplos proporcionan y modificación la plantilla para sus necesidades.

## <a name="step-3-deploy-resources-with-powershell"></a>Paso 3: Implementación de los recursos con PowerShell
Después de que ha personalizado las plantillas y los scripts, siga los pasos de hello necesarios demasiado[implementar los recursos con plantillas de administrador de recursos y Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy). artículo de Hello proporciona información general sobre el uso de PowerShell de Azure con Azure Resource Manager plantillas toodeploy su tooAzure de recursos.


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a>Tareas comunes que puede realizar en DevTest Labs con PowerShell
Hay muchas otras tareas habituales que puede automatizar mediante PowerShell. Hello siguientes secciones de documentación de hello presentan Hola pasos necesario tooperform estas tareas.

* [Creación de una imagen personalizada a partir de un archivo VHD mediante PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [Cargar la cuenta de almacenamiento del toolab del archivo de disco duro virtual con PowerShell](devtest-lab-upload-vhd-using-powershell.md)
* [Agregar un laboratorio de tooa de usuario externo con PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [Creación de un rol personalizado de laboratorio con PowerShell](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo toocreate una [repositorio Git privado](devtest-lab-add-artifact-repo.md) donde se almacenarán los plantillas personalizadas o scripts.
* Explorar hello [plantillas del Administrador de recursos de Azure desde la Galería de plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates).
