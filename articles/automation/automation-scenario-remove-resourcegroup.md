---
title: "eliminación de aaaAutomate de grupos de recursos | Documentos de Microsoft"
description: "Versión de flujo de trabajo de PowerShell de un escenario de automatización de Azure incluidos runbooks tooremove grupos de todos los recursos en su suscripción."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: 
ms.assetid: b848e345-fd5d-4b9d-bc57-3fe41d2ddb5c
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/26/2016
ms.author: magoedte
ms.openlocfilehash: d7ff8064842385d57b0eebdf7b263150c958255f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automate-removal-of-resource-groups"></a>Escenario de Azure Automation: automatizar la eliminación de grupos de recursos
Muchos clientes crean más de un grupo de recursos. Algunos se podrían usar para administrar aplicaciones de producción y otros como entornos de desarrollo, pruebas y ensayo. Automatizar la implementación de Hola de estos recursos es algo, pero que se va a toodecommission capaz de un grupo de recursos con un clic del botón de hello es otra. Esta tarea común de administración se puede optimizar mediante Azure Automation. Esto resulta útil si está trabajando con una suscripción de Azure que tiene un límite de gasto a través de una oferta de miembro como MSDN u Hola programa Microsoft Partner Network Cloud Essentials.

Este escenario se basa en un runbook de PowerShell y está diseñada tooremove uno o varios grupos de recursos que especifique desde su suscripción. configuración predeterminada de Hola de runbook de hello es tootest antes de continuar. Esto garantiza que no elimina el grupo de recursos de Hola antes de haber preparado toocomplete este procedimiento.   

## <a name="getting-hello-scenario"></a>Introducción al escenario de Hola
Este escenario consta de un runbook de PowerShell que puede descargar desde hello [Galería de PowerShell](https://www.powershellgallery.com/packages/Remove-ResourceGroup/1.0/DisplayScript). También puede importar directamente desde hello [Galería de runbooks](automation-runbook-gallery.md) Hola portal de Azure.<br><br>

| Runbook | Description |
| --- | --- |
| Remove-ResourceGroup |Quita uno o más grupos de recursos de Azure y recursos asociados de suscripción de Hola. |

<br>
Hola parámetros de entrada siguientes se define para este runbook:

| Parámetro | Description |
| --- | --- |
| NameFilter (obligatorio) |Especifica el nombre toolimit Hola recursos grupos de filtro que piensa sobre cómo eliminar. Puede pasar varios valores mediante una lista separada por comas.<br>filtro de Hello no distingue mayúsculas de minúsculas y coincidirá con cualquier grupo de recursos que contiene la cadena de Hola. |
| PreviewMode (opcional) |Ejecuta Hola runbook toosee qué grupos de recursos se eliminarán, pero no realiza ninguna acción.<br>valor predeterminado de Hello es **true** toohelp evitar la eliminación accidental de uno o más grupos de recursos pasan toohello runbook. |

## <a name="install-and-configure-this-scenario"></a>Instalación y configuración de este escenario
### <a name="prerequisites"></a>Requisitos previos
Este runbook autentica mediante hello [cuenta de identificación de Azure](automation-sec-configure-azure-runas-account.md).    

### <a name="install-and-publish-hello-runbooks"></a>Instalar y publicar runbooks Hola
Después de descargar Hola runbook, puede importarlo mediante procedimiento hello en [importar runbook procedimientos](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation). Publicar Hola runbook después de se ha importado correctamente en su cuenta de automatización.

## <a name="using-hello-runbook"></a>Uso de hello runbook
Hello siguientes pasos le guiarán a través de la ejecución de Hola de este runbook y ayudarán a familiarizarse con su funcionamiento. Va a solo probar Hola runbook en este ejemplo, no eliminar grupo de recursos de Hola.  

1. De hello portal de Azure, abra su cuenta de automatización y haga clic en **Runbooks**.
2. Seleccione hello **Remove-ResourceGroup** runbook y haga clic en **iniciar**.
3. Cuando se inicia el runbook de hello, Hola **iniciar Runbook** hoja se abre y puede configurar los parámetros de Hola. Escriba los nombres de Hola de grupos de recursos en la suscripción que puede usar para realizar pruebas y no provocará ningún daño si elimina accidentalmente.<br> ![Remove-ResouceGroup parameters](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-input-parameters.png)

   > [!NOTE]
   > Asegúrese de que **Previewmode** se establece demasiado**true** tooavoid eliminar Hola seleccionado grupos de recursos.  **Tenga en cuenta** que este runbook no quitará el grupo de recursos de Hola que contiene la cuenta de automatización de Hola que se está ejecutando este runbook.  
   >
   >
4. Después de haber configurado todos los valores de parámetro de hello, haga clic en **Aceptar**, y Hola runbook se pondrá en cola para su ejecución.  

detalles de hello tooview de hello **quitar grupo de recursos** trabajo de runbook en hello portal de Azure, seleccione **trabajos** Hola runbook. parámetros de entrada de Hello trabajo proporciona resúmenes hello y salida de hello secuencia además toogeneral información sobre el trabajo de Hola y cualquier excepción que se ha producido.<br> ![Estado del trabajo del Runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-status.png).

Hola **resumen del trabajo** incluye mensajes de secuencias de salida, advertencia y error de Hola. Seleccione **salida** tooview obtener resultados de ejecución de un runbook Hola.<br> ![Resultados de la salida del Runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-output.png)

## <a name="next-steps"></a>Pasos siguientes
* tooget de partida para crear su propio runbook, consulte [crear o importar un runbook en automatización de Azure](automation-creating-importing-runbook.md).
* tooget a trabajar con runbooks de flujo de trabajo de PowerShell, consulte [mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md).
