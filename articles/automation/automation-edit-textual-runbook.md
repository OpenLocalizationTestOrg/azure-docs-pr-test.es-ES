---
title: "aaaEditing textual runbooks en automatización de Azure"
description: "Este artículo proporciona diferentes procedimientos para trabajar con runbooks de flujo de trabajo de PowerShell y PowerShell en automatización de Azure mediante el editor de texto hello."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 6f5b48fb-6f30-4e99-9e14-9061b5554b08
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 3fd87d457838f300ca6c94bc345e82c679a0e011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="editing-textual-runbooks-in-azure-automation"></a>Edición de runbooks de texto en Automatización de Azure
Hello editor de texto de automatización de Azure puede ser usado tooedit [runbooks PowerShell](automation-runbook-types.md#powershell-runbooks) y [runbooks de flujo de trabajo de PowerShell](automation-runbook-types.md#powershell-workflow-runbooks). Esto tiene las características típicas de otros editores de código, como intellisense y codificación de colores con características especiales adicionales tooassist también en obtener acceso a recursos comunes toorunbooks Hola.  En este artículo, se proporcionan pasos detallados para realizar diferentes funciones con este editor.

editor de texto Hello incluye un código de tooinsert de característica para actividades, activos y runbooks secundarios en un runbook. En lugar de escribir código de hello, puede seleccionar de una lista de recursos disponibles y tienen Hola inserte código adecuado en hello runbook.

Cada runbook de Automatización de Azure tiene dos versiones: una de borrador y otra publicada. Editar Hola versión de borrador de runbook de hello y, a continuación, publicarlo para que se pueda ejecutar. no se puede editar la versión publicada de Hola. Consulte el artículo sobre la [publicación de un runbook](automation-creating-importing-runbook.md#publishing-a-runbook) para obtener más información.

toowork con [Runbooks gráficos](automation-runbook-types.md#graphical-runbooks), consulte [edición gráfica en automatización de Azure](automation-graphical-authoring-intro.md).

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit un runbook con hello portal de Azure
Usar hello siguiendo el procedimiento tooopen un runbook para modificarlo en el editor de texto hello.

1. Hola portal de Azure, seleccione su cuenta de automatización.
2. Haga clic en hello **Runbooks** icono tooopen Hola lista de runbooks.
3. Haga clic en el nombre de Hola de hello runbook que desee tooedit y, a continuación, haga clic en hello **editar** botón.
4. Realizar Hola necesario editar.
5. Haga clic en **Guardar** cuando termine las modificaciones.
6. Haga clic en **publicar** si desea Hola última versión de borrador Hola runbook toobe publicado.

### <a name="tooinsert-a-cmdlet-into-a-runbook"></a>tooinsert un cmdlet en un runbook
1. Hola lienzo del editor de texto hello, coloque cursor Hola donde desea tooplace Hola cmdlet.
2. Expanda hello **Cmdlets** nodo Hola control de la biblioteca.
3. Expanda módulo Hola que contiene cmdlet Hola desea toouse.
4. Haga clic en hello cmdlet tooinsert y seleccione **agregar toocanvas**.  Si el cmdlet de hello tiene más de un parámetro establecido, se agregará conjunto predeterminado de Hola.  También puede expandir Hola cmdlet tooselect otro parámetro de conjunto.
5. código de Hello para el cmdlet de Hola se inserta con toda su lista de parámetros.
6. Proporcione un valor adecuado en lugar del tipo de datos de hello entre llaves <> para los parámetros necesarios.  Elimine cualquier parámetro que no sea necesario.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>código de tooinsert para un runbook secundario en un runbook
1. Hola lienzo del editor de texto hello, sitúe cursor Hola donde desee que código de hello tooplace para hello [runbook secundario](automation-child-runbooks.md).
2. Expanda hello **Runbooks** nodo Hola control de la biblioteca.
3. Haga clic en hello runbook tooinsert y seleccione **agregar toocanvas**.
4. código de Hello runbook secundario se Hola se inserta con los marcadores de posición para los parámetros de runbook.
5. Reemplace los marcadores de posición de hello con los valores adecuados para cada parámetro.

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert un recurso en un runbook
1. En el lienzo del editor de texto de Hola Hola, sitúe cursor Hola donde desee que código de hello tooplace runbook secundario se Hola.
2. Expanda hello **activos** nodo Hola control de la biblioteca.
3. Expanda el nodo de hello para el tipo de saludo del recurso que desee.
4. Haga clic en hello asset tooinsert y seleccione **agregar toocanvas**.  Para [activos variable](automation-variables.md), seleccione **agregar "Obtener Variable" toocanvas** o **agregar "Set Variable" toocanvas** dependiendo de si desea tooget o establecer variable de saludo.
5. se inserta código de Hello para el activo de hello en hello runbook.

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit un runbook con hello portal de Azure
Usar hello siguiendo el procedimiento tooopen un runbook para modificarlo en el editor de texto hello.

1. Hola portal de Azure, seleccione **automatización** y, a continuación, haga clic en nombre de Hola de una cuenta de automatización.
2. Seleccione hello **Runbooks** ficha.
3. Haga clic en el nombre de Hola de hello runbook que desee tooedit y, a continuación, seleccione hello **autor** ficha.
4. Haga clic en hello **editar** situado en la parte inferior de Hola de pantalla de bienvenida.
5. Realizar Hola necesario editar.
6. Haga clic en **Guardar** cuando termine las modificaciones.
7. Haga clic en **publicar** si desea Hola última versión de borrador Hola runbook toobe publicado.

### <a name="tooinsert-an-activity-into-a-runbook"></a>tooinsert una actividad en un Runbook
1. Hola lienzo del editor de texto hello, coloque cursor Hola donde desea tooplace Hola actividad.
2. En la parte inferior de Hola de pantalla de bienvenida, haga clic en **insertar** y, a continuación, **actividad**.
3. Hola **módulo de integración** columna, el módulo de hello select que contiene la actividad hello.
4. Hola **actividad** panel, seleccione una actividad.
5. Hola **descripción** columna, descripción de Hola de nota de actividad de Hola. Si lo desea, puede hacer clic en vista detallada de la Ayuda toolaunch ayuda para la actividad de hello en el Explorador de Hola.
6. Haga clic en la flecha derecha Hola.  Si la actividad hello tiene parámetros, se enumerarán para su información.
7. Haga clic en el botón de comprobación de Hola.  Actividad de hello toorun de código se insertará en hello runbook.
8. Si la actividad de hello requiere parámetros, proporcione un valor adecuado en lugar del tipo de datos de hello entre llaves <>.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>código de tooinsert para un runbook secundario en un runbook
1. Hola lienzo del editor de texto hello, coloque cursor Hola donde desee hello tooplace [runbook secundario](automation-child-runbooks.md).
2. En la parte inferior de Hola de pantalla de bienvenida, haga clic en **insertar** y, a continuación, **Runbook**.
3. Seleccione Hola runbook tooinsert de la columna central de Hola y haga clic en la flecha derecha de Hola.
4. Si Hola runbook tiene parámetros, se enumerarán para su información.
5. Haga clic en el botón de comprobación de Hola.  Código toorun Hola seleccionado runbook se insertará en el runbook actual Hola.
6. Si Hola runbook requiere parámetros, proporcione un valor adecuado en lugar del tipo de datos de hello entre llaves <>.

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert un recurso en un runbook
1. Hola lienzo del editor de texto hello, colocar cursor Hola donde desea activos de tooplace Hola actividad tooretrieve Hola.
2. En la parte inferior de Hola de pantalla de bienvenida, haga clic en **insertar** y, a continuación, **configuración**.
3. Hola **acción de configuración** columna, acción seleccione Hola que desee.
4. Seleccione entre Hola activos disponibles en la columna central de Hola.
5. Haga clic en el botón de comprobación de Hola.  Código tooget o conjunto Hola activos se insertará en hello runbook.

## <a name="tooedit-an-azure-automation-runbook-using-windows-powershell"></a>tooedit un runbook de automatización de Azure con Windows PowerShell
tooedit un runbook con Windows PowerShell, utiliza el editor Hola de su elección y guardar archivo. ps1 de tooa. Puede usar hello [Get-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/getazurerunbookdefinition) contenido de hello tooretrieve de cmdlet de runbook de hello y, a continuación, [Set-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/setazurerunbookdefinition) cmdlet tooreplace Hola existente runbook de borrador con hello había modificado uno.

### <a name="tooretrieve-hello-contents-of-a-runbook-using-windows-powershell"></a>tooRetrieve Hola contenido de un Runbook mediante Windows PowerShell
Hola después de comandos de ejemplo muestra cómo tooretrieve Hola script para un runbook y guardar archivo de script de tooa. En este ejemplo, se recupera la versión de borrador de Hola. También es posible tooretrieve Hola publicada versión de Hola runbook aunque no se puede cambiar esta versión.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    $runbookDefinition = Get-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Slot Draft
    $runbookContent = $runbookDefinition.Content

    Out-File -InputObject $runbookContent -FilePath $scriptPath

### <a name="toochange-hello-contents-of-a-runbook-using-windows-powershell"></a>tooChange Hola contenido de un Runbook mediante Windows PowerShell
Hello comandos de ejemplo siguientes muestran cómo tooreplace Hola contenido existente de un runbook con contenido de Hola de un archivo de script. Tenga en cuenta que esto es Hola mismo ejemplo del procedimiento como en [tooimport un runbook desde un archivo de script con Windows PowerShell](automation-creating-importing-runbook.md).

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    Set-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Path $scriptPath -Overwrite
    Publish-AzureAutomationRunbook –AutomationAccountName $automationAccountName –Name $runbookName

## <a name="related-articles"></a>Artículos relacionados
* [Creación o importación de un runbook en Automatización de Azure](automation-creating-importing-runbook.md)
* [Aprendizaje del flujo de trabajo de Windows PowerShell](automation-powershell-workflow.md)
* [Creación gráfica en Automatización de Azure](automation-graphical-authoring-intro.md)
* [Certificados](automation-certificates.md)
* [Conexiones](automation-connections.md)
* [Credenciales](automation-credentials.md)
* [Programaciones](automation-schedules.md)
* [Variables](automation-variables.md)
