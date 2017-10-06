---
title: "configuración de aaaRunbook | Documentos de Microsoft"
description: "Describe los valores de configuración de Hola para un runbook en automatización de Azure y cómo toochange con ambos Hola Portal de administración de Azure y Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a>Configuración de runbook
Cada runbook de automatización de Azure tiene varias opciones de configuración para facilitar su toobe identificado y toochange su comportamiento de registro. Cada uno de estos valores se describe a continuación los procedimientos sobre cómo toomodify ellos.

## <a name="settings"></a>Settings
### <a name="name-and-description"></a>Nombre y descripción
No se puede cambiar nombre de Hola de un runbook una vez creada. Hola descripción es opcional y puede ser too512 caracteres.

### <a name="tags"></a>Etiquetas
Las etiquetas permiten que tooassign diferentes palabras y frases toohelp identifican un runbook. Por ejemplo, cuando se envía un runbook toohello [Galería de PowerShell](https://www.powershellgallery.com/), especifique tooidentify etiquetas determinado qué categorías de Hola runbook debe aparecer en. Puede especificar varias etiquetas para un runbook separándolas por comas.

### <a name="logging"></a>Registro
De forma predeterminada, los registros detallado y de progreso no se escriben toojob historial. Puede cambiar valores de hello para un runbook determinado toolog estos registros. Para obtener más información sobre estos registros, consulte [Salida y mensajes de los runbooks](automation-runbook-output-and-messages.md).

## <a name="changing-runbook-settings"></a>Cambio de la configuración del runbook

### <a name="changing-runbook-settings-with-hello-azure-portal"></a>Cambiar la configuración de runbook con hello portal de Azure
Puede cambiar la configuración de un runbook en hello portal de Azure de hello **configuración** hoja Hola runbook.

1. Hola portal de Azure, seleccione **automatización** y, a continuación, haga clic en nombre de Hola de una cuenta de automatización.
2. Seleccione hello **Runbooks** ficha.
3. Haga clic en nombre de Hola de un runbook y son toohello dirigido hoja de configuración de runbook de Hola. Desde aquí puede especificar o modificar etiquetas, Hola descripción del runbook, configurar el registro y la configuración de seguimiento y tener acceso a solucionar problemas de compatibilidad con herramientas toohelp.     

### <a name="changing-runbook-settings-with-windows-powershell"></a>Cambio de la configuración del runbook mediante Windows PowerShell
Puede usar hello [AzureRmAutomationRunbook conjunto](https://msdn.microsoft.com/library/mt603786.aspx) configuración de cmdlet toochange Hola de un runbook. Si desea toospecify varias etiquetas, se puede proporcionar una matriz o una sola cadena con el parámetro de etiquetas de toohello de valores delimitada por comas. Puede obtener etiquetas actuales de hello con hello [AzureRmAutomationRunbook Get](https://msdn.microsoft.com/library/mt603728.aspx).

Hola después de comandos de ejemplo muestra cómo tooset Hola propiedades de un runbook. Este ejemplo agrega tres etiquetas toohello existente etiquetas y especifica que se deben registrar registros detallados.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a>Pasos siguientes
* toolearn toocreate y recuperar mensajes de error y de salida de runbooks, vea [Runbook Output and Messages](automation-runbook-output-and-messages.md) 
* toounderstand cómo ver un runbook que ya se haya desarrollado por hello Comunidad otro origen o toocreate su propio runbook tooadd [crear o importar un Runbook](automation-creating-importing-runbook.md) 

