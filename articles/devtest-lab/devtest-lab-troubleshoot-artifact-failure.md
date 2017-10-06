---
title: errores de artefacto aaaDiagnose en VM de laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tootroubleshoot errores de artefactos en los laboratorios de desarrollo y pruebas"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: tarcher
ms.openlocfilehash: 40b3cea72cf071cc5d9a6d002d309d923c3d3084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-artifact-failures-in-hello-lab"></a>Diagnosticar errores de artefacto en laboratorio Hola 
Después de haber creado un artefacto, puede comprobar toosee si realizó correctamente o no. Registros de artefactos en los laboratorios de desarrollo y pruebas proporcionan información que puede usar toodiagnose un error de artefacto. Hay un par de formas diferentes puede ver la información de registro de hello artefacto de una VM de Windows.

> [!NOTE]
> tooensure que los errores correctamente se identifican y se ha explicado, es importante ese artefacto Hola está estructurado correctamente. Para obtener información acerca de cómo toocorrectly crea un artefacto, consulte [crear artefactos personalizados](devtest-lab-artifact-author.md). Y toosee un ejemplo de un artefacto correctamente estructurado, consulte esta [tipos de parámetros de prueba](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artefacto.

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a>Solucionar problemas de errores de artefacto mediante Hola portal de Azure
errores de Azure toodiagnose portal toouse Hola durante la creación de artefacto, siga estos pasos:

1. En lista de Hola de recursos, seleccione el laboratorio.

2. Elija Hola VM de Windows que incluye el artefacto de hello desea tooinvestigate.

3. En el panel izquierdo de hello en **GENERAL**, elija **artefactos**. Aparece una lista de artefactos asociados a esa máquina virtual, lo que indica nombre Hola de artefacto de Hola y su estado.

   ![Ejemplo de repositorio de Git de artefacto](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. Elija un artefacto que muestre un estado de **Con error**. artefacto de Hola se abre y muestra un mensaje de extensión que incluye detalles sobre los errores de Hola de artefacto de Hola.

   ![Ejemplo de repositorio de Git de artefacto](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a>Solucionar errores de artefactos desde dentro de hello VM
los registros de artefacto de Hola de tooview desde dentro de la máquina virtual de hello, siga estos pasos:

1. Inicie sesión en la máquina virtual que contiene el artefacto de hello desea toodiagnose toohello.

2. Navegue tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status donde "1.9 es el número de versión de Hola CSE.

   ![Ejemplo de repositorio de Git de artefacto](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. Abra hello **estado** archivo tooview la información que ayuda a diagnosticar errores de artefacto de esa máquina virtual.




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Entradas blogs relacionadas
* [Unirse a un dominio de Active Directory mediante una plantilla de administrador de recursos en los laboratorios de desarrollo y pruebas de Azure tooexisting VM](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[agregar un laboratorio de tooa del repositorio de Git](devtest-lab-add-artifact-repo.md).

