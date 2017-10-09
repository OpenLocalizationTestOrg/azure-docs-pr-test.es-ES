---
title: plantillas de aaaDeploy con Visual Studio en la pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodeploy plantillas con Visual Studio en la pila de Azure."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 628da2ae-64cc-42e0-b8b7-a6a3724cb974
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: aea917b585a30ef4fbe7263db66f0659b56b21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-visual-studio"></a>Implementación de plantillas en Azure Stack con Visual Studio

Utilice las kit de desarrollo de Visual Studio toodeploy Azure Resource Manager plantillas toohello pila de Azure.

1. [Instalar y conectar](azure-stack-install-visual-studio.md) tooAzure pila con Visual Studio.
2. Abra Visual Studio.
3. Haga clic en **archivo**, haga clic en **New**y en hello **nuevo proyecto** haga clic en el cuadro de diálogo **grupo de recursos de Azure**.
4. Escriba un **nombre** para hello nuevos proyectos y, a continuación, haga clic en **Aceptar**.
5. Hola **Seleccionar plantilla de Azure** cuadro de diálogo, cambio hello *mostrar plantillas desde esta ubicación* desplegable demasiado**inicio rápido de pila de Azure**
6. Haga clic en **101-create-storage-account** y, después, haga clic en **Aceptar**.  
7. En el proyecto nuevo, puede ver una lista de plantillas de hello disponibles expandiendo hello **plantillas** nodo Hola **el Explorador de soluciones** panel.
8. Hola **el Explorador de soluciones** panel, nombre de Hola de menú contextual del proyecto, haga clic en **implementar**, a continuación, haga clic en **nueva implementación**.
9. Hola **implementar tooResource grupo** cuadro de diálogo hello **suscripción** lista desplegable, seleccione la suscripción de la pila de Microsoft Azure.
10. Hola **grupo de recursos** lista, elija un grupo de recursos existente o cree uno nuevo.
11. Hola **ubicación del grupo de recursos** lista, elija una ubicación y, a continuación, haga clic en **implementar**.
12. Hola **editar parámetros** diálogo cuadro, escriba valores para los parámetros de hello (que varían según la plantilla) y, a continuación, haga clic en **guardar**.

## <a name="next-steps"></a>Pasos siguientes
[Implementación de plantillas de línea de comandos de Hola](azure-stack-deploy-template-command-line.md)

[Desarrollo de plantillas para Azure Stack](azure-stack-develop-templates.md)

