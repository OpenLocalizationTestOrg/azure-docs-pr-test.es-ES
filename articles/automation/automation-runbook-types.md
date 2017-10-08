---
title: "aaaAzure tipos de Runbook de automatización | Documentos de Microsoft"
description: "Describe diferentes tipos de Hola de runbooks que puede usar en automatización de Azure y las consideraciones que debe tener en cuenta al determinar qué toouse de tipo. "
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9265c975-4281-4819-a84f-d86641277f36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/01/2017
ms.author: bwren
ms.openlocfilehash: c28aa57c77025764b16784372308a4ff2f596914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-runbook-types"></a>Tipos de runbooks de Automatización de Azure
Automatización de Azure admite cuatro tipos de runbooks que se describen brevemente en hello en la tabla siguiente.  Hello las siguientes secciones proporcionan más información sobre cada tipo incluidas consideraciones sobre cuándo toouse cada.

| Tipo | Description |
|:--- |:--- |
| [Gráfico](#graphical-runbooks) |Basado en Windows PowerShell y creado y editado completamente en el editor gráfico del Portal de Azure. |
| [Flujo de trabajo gráfico de PowerShell](#graphical-runbooks) |Se basa en el flujo de trabajo de Windows PowerShell y editor gráfico de creados y editados por completo en hello en el portal de Azure. |
| [PowerShell](#powershell-runbooks) |Runbook de texto basado en el script de Windows PowerShell. |
| [Flujo de trabajo de PowerShell](#powershell-workflow-runbooks) |Runbook de texto basado en el flujo de trabajo de Windows PowerShell. |

## <a name="graphical-runbooks"></a>Runbooks gráficos
[Gráfico](automation-runbook-types.md#graphical-runbooks) y flujo de trabajo de PowerShell gráfica runbooks creados y editados con el editor gráfico de Hola Hola portal de Azure.  Puede exportarlos tooa archivo y, a continuación, importarlos en otra cuenta de automatización, pero no puede crear o editar con otra herramienta.  Runbooks gráficos generan código de PowerShell, pero no puede ver o modificar el código de hello directamente. Runbooks gráficos no se puede convertir tooone de hello [formatos de texto](automation-runbook-types.md), ni puede ser un runbook de texto convertido toographical formato. Runbooks gráficos puede ser convertido tooGraphical runbooks de flujo de trabajo de PowerShell durante la importación y viceversa.

### <a name="advantages"></a>Ventajas
* Modelo de creación visual para insertar, vincular y configurar.  
* Centrarse en cómo fluyen los datos a través del proceso de Hola  
* Representa visualmente los procesos de administración.  
* Incluir otros runbooks como secundarios runbooks toocreate alto nivel flujos de trabajo  
* Anima a usar la programación modular.  


### <a name="limitations"></a>Limitaciones
* No se pueden editar los runbooks fuera del Portal de Azure.
* Puede requerir una actividad de código que contiene la lógica compleja de tooperform de código de PowerShell.
* No puede ver ni modificar directamente código de PowerShell de hello creado por flujo de trabajo gráfico de Hola. Tenga en cuenta que puede ver código de hello que crear en las actividades de código.

## <a name="powershell-runbooks"></a>Runbooks de PowerShell
Los runbooks de PowerShell están basados en Windows PowerShell.  Editar directamente código de hello de runbook de hello con el editor de texto de Hola Hola portal de Azure.  También puede usar cualquier editor de texto sin conexión y [importar runbook hello](http://msdn.microsoft.com/library/azure/dn643637.aspx) en automatización de Azure.

### <a name="advantages"></a>Ventajas
* Implementar toda la lógica compleja con código de PowerShell sin las complejidades adicionales de Hola de flujo de trabajo de PowerShell. 
* Runbook se inicia más rápidamente que los runbooks de flujo de trabajo de PowerShell porque no es necesario toobe compilado antes de ejecutar.

### <a name="limitations"></a>Limitaciones
* Debe estar familiarizado con el scripting de PowerShell.
* No se puede usar [procesamiento en paralelo](automation-powershell-workflow.md#parallel-processing) tooperform varias acciones en paralelo.
* No se puede usar [puntos de comprobación](automation-powershell-workflow.md#checkpoints) tooresume runbook en caso de error.
* Runbooks de flujo de trabajo de PowerShell y runbooks gráficos solo pueden incluidos como runbooks secundarios usando el cmdlet Start-AzureAutomationRunbook Hola que crea un nuevo trabajo.

### <a name="known-issues"></a>Problemas conocidos
A continuación se describen los problemas conocidos actuales con runbooks de PowerShell.

* Los runbooks de PowerShell no pueden recuperar un [activo de variables](automation-variables.md) sin cifrar con un valor null.
* No se puede recuperar runbooks PowerShell un [activo de variable](automation-variables.md) con  *~*  en nombre de Hola.
* Get-Process en un bucle de un runbook de PowerShell puede bloquearse después de más de 80 iteraciones. 
* Un runbook de PowerShell puede producir un error si intenta toowrite una gran cantidad de flujo de salida de toohello de datos a la vez.   Normalmente puede solucionar este problema al generar únicamente información de hello que necesaria cuando se trabaja con objetos grandes.  Por ejemplo, en lugar de generar algo parecido a *Get-Process*, puedes obtener una salida sólo los campos de hello necesario con *Get-Process | Seleccione ProcessName, CPU*.

## <a name="powershell-workflow-runbooks"></a>Runbooks del flujo de trabajo de PowerShell
Los runbooks del flujo de trabajo de PowerShell son runbooks de texto basados en el [flujo de trabajo de Windows PowerShell](automation-powershell-workflow.md).  Editar directamente código de hello de runbook de hello con el editor de texto de Hola Hola portal de Azure.  También puede usar cualquier editor de texto sin conexión y [importar runbook hello](http://msdn.microsoft.com/library/azure/dn643637.aspx) en automatización de Azure.

### <a name="advantages"></a>Ventajas
* Implemente toda la lógica compleja con código del flujo de trabajo de PowerShell.
* Use [puntos de comprobación](automation-powershell-workflow.md#checkpoints) tooresume runbook en caso de error.
* Use [procesamiento en paralelo](automation-powershell-workflow.md#parallel-processing) tooperform varias acciones en paralelo.
* Puede incluir otros runbooks gráficos y runbooks de flujo de trabajo de PowerShell como secundarios runbooks toocreate alto nivel flujos de trabajo.

### <a name="limitations"></a>Limitaciones
* El autor debe estar familiarizado con el flujo de trabajo de PowerShell.
* Runbook debe tratar Hola complejidad adicional de flujo de trabajo de PowerShell como [deserializar objetos](automation-powershell-workflow.md#code-changes).
* Runbook toma más toostart de runbooks de PowerShell que puesto que necesita toobe compilado antes de ejecutar.
* PowerShell runbooks solo pueden incluidos como runbooks secundarios usando el cmdlet Start-AzureAutomationRunbook Hola que crea un nuevo trabajo.

## <a name="considerations"></a>Consideraciones
También debe tener en hello cuenta las siguientes consideraciones adicionales cuando determinar qué toouse de tipo de un runbook determinado.

* No se puede convertir runbooks del tipo de gráfico tootextual o viceversa.
* Existen limitaciones al usar runbooks de diferentes tipos como runbooks secundarios.  Consulte [Runbooks secundarios en la Automatización de Azure](automation-child-runbooks.md) para obtener más información.

## <a name="next-steps"></a>Pasos siguientes
* toolearn más información acerca de la creación de runbooks gráficos, consulte [creación gráfica en automatización de Azure](automation-graphical-authoring-intro.md)
* Hola toounderstand diferencias entre PowerShell y PowerShell flujos de trabajo de runbooks, vea [el flujo de trabajo de aprendizaje Windows PowerShell](automation-powershell-workflow.md)
* Para obtener más información sobre cómo toocreate o importar un Runbook, consulte [crear o importar un Runbook](automation-creating-importing-runbook.md)

