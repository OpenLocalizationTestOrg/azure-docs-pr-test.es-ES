---
title: "aaaUpdate Azure módulos de automatización de Azure | Documentos de Microsoft"
description: "En este artículo se describe cómo puede actualizar ahora módulos comunes de Azure PowerShell proporcionados de forma predeterminada en Azure Automation."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a>¿Cómo tooupdate módulos de PowerShell de Azure en automatización de Azure

módulos de PowerShell de Azure más comunes de Hola se proporcionan de forma predeterminada en cada cuenta de automatización.  las actualizaciones del equipo de Azure de Hola Hola módulos de Azure con regularidad, por lo que en hello cuenta de automatización se proporcionan una manera para tooupdate módulos de hello en la cuenta de hello cuando estén disponibles desde el portal de hello las nuevas versiones.  

Debido a los módulos se actualizan periódicamente por grupo de producto de hello, pueden producirse cambios con los cmdlets de hello incluida, lo que puede afectar negativamente sus runbooks según tipo hello de cambo, como cambiar el nombre de un parámetro o dejando un cmdlet completamente. tooavoid que afectan a los runbooks y Hola procesos automatizan, se recomienda encarecidamente que probar y validar antes de continuar.  Si no tiene una cuenta de automatización dedicada diseñada para este propósito, considere la posibilidad de crear uno para que pueda probar muchos escenarios diferentes y permutaciones durante el desarrollo de Hola de sus runbooks, cambios de tooiterative de suma, como la actualización Hola Módulos de PowerShell.  Después de que se validan los resultados de Hola y se les aplique los cambios necesarios, continuar con la migración Hola de los runbooks que requieren la modificación de coordinar y realizar la actualización de hello tal y como se describe a continuación en producción.     

## <a name="updating-azure-modules"></a>Actualización de módulos de Azure

1. En los módulos de hello hoja de la cuenta de automatización no existe es una opción denominada **módulos de Azure Update**.  Siempre está habilitada.<br><br> ![Opción Update Azure Modules (Actualizar módulos de Azure) en la hoja Módulos](media/automation-update-azure-modules/automation-update-azure-modules-option.png)

2. Haga clic en **módulos de Azure Update** y aparecerá una notificación de confirmación que le pregunta si desea toocontinue.<br><br> ![Notificación de Update Azure Modules (Actualizar módulos de Azure)](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)

3. Haga clic en **Sí** y se iniciará el proceso de actualización del módulo de Hola.  proceso de actualización de Hello tarda aproximadamente Hola de tooupdate 15-20 minutos siguientes módulos:

  * Azure
  * Azure.Storage
  * AzureRm.Automation
  * AzureRm.Compute
  * AzureRm.Profile
  * AzureRm.Resources
  * AzureRm.Sql
  * AzureRm.Storage

    Si los módulos de hello ya están en marcha toodate, proceso de Hola se completará en unos segundos.  Cuando se completa el proceso de actualización de Hola se le notificará.<br><br> ![Estado de actualización de Update Azure Modules (Actualizar módulos de Azure)](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> Automatización de Azure utilizará módulos más recientes de hello en su cuenta de automatización cuando se ejecuta un nuevo trabajo programado.    

Si usa cmdlets de estos módulos de PowerShell de Azure en su toomanage runbooks Azure recursos, es recomendable tooperform este proceso de actualización de cada mes o por lo que tooassure que tienes bienvenida módulos más recientes.

## <a name="next-steps"></a>Pasos siguientes

* toolearn más información acerca de los módulos de integración y cómo integrar toocreate módulos personalizados toofurther la automatización con otros sistemas, servicios o soluciones, consulte [módulos de integración](automation-integration-modules.md).

* Considere el uso de la integración de control de origen [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) o [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally administrar y controlar las versiones de la cartera de runbook y la configuración de automatización.  
