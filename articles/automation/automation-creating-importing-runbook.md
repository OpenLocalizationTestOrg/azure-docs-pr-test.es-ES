---
title: "aaaCreating o importar un runbook en automatización de Azure"
description: "Este artículo se describe cómo toocreate un nuevo runbook en automatización de Azure o importar desde un archivo."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 24414362-b690-4474-8ca7-df18e30fc31d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d45f44cf15fbcacdd0de2977668502c2e1671063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-or-importing-a-runbook-in-azure-automation"></a>Creación o importación de un runbook en Azure Automation
Puede agregar un runbook tooAzure automatización, ya sea [crear una nueva](#creating-a-new-runbook) o importando un runbook existente desde un archivo o de hello [Galería de runbooks](automation-runbook-gallery.md). Este artículo ofrece información sobre cómo crear e importar runbooks de un archivo.  Puede obtener todos los detalles de hello sobre cómo acceder a la Comunidad runbooks y módulos en [galerías de módulos y runbooks de automatización de Azure](automation-runbook-gallery.md).

## <a name="creating-a-new-runbook"></a>Creación de un nuevo runbook
Puede crear un nuevo runbook en automatización de Azure mediante uno de hello Azure portales o Windows PowerShell. Una vez que se ha creado el runbook de hello, puede editar siguiendo la información en [el flujo de trabajo de aprendizaje PowerShell](automation-powershell-workflow.md) y [edición gráfica en automatización de Azure](automation-graphical-authoring-intro.md).

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-classic-portal"></a>toocreate un nuevo runbook de automatización de Azure con el portal de Azure clásico de Hola
Sólo se puede trabajar con [runbooks de flujo de trabajo de PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) Hola portal de Azure.

1. En el portal de Azure clásico de hello, haga clic en, **New**, **servicios de aplicaciones**, **automatización**, **Runbook**, **creaciónrápida**.
2. Escriba información de hello necesario y, a continuación, haga clic en **crear**. nombre de runbook de Hello debe empezar por una letra y puede contener letras, números, caracteres de subrayado y guiones.
3. Si desea tooedit Hola runbook ahora, a continuación, haga clic en **editar Runbook**. De lo contrario, haga clic en **Aceptar**.
4. El nuevo runbook aparecerá en hello **Runbooks** ficha.

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-portal"></a>toocreate un nuevo runbook de automatización de Azure con hello portal de Azure
1. Hola portal de Azure, abra su cuenta de automatización.
2. En hello concentrador, seleccione **Runbooks** tooopen lista de Hola de runbooks.
3. Haga clic en hello **agregar un runbook** botón y, a continuación, **crear un nuevo runbook**.
4. Escriba un **nombre** de runbook de Hola y seleccione su [tipo](automation-runbook-types.md). nombre de runbook de Hello debe empezar por una letra y puede contener letras, números, caracteres de subrayado y guiones.
5. Haga clic en **crear** toocreate Hola runbook y editor Hola abierto.

### <a name="toocreate-a-new-azure-automation-runbook-with-windows-powershell"></a>toocreate un nuevo runbook de automatización de Azure con Windows PowerShell
Puede usar hello [New-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) toocreate cmdlet vacío [runbook de flujo de trabajo de PowerShell](automation-runbook-types.md#powershell-workflow-runbooks). Puede especificar hello **nombre** toocreate parámetro un runbook vacío que pueda modificar más adelante, o puede especificar hello **ruta de acceso** parámetro tooimport un archivo de runbook. Hola **tipo** parámetro también debe ser toospecify incluye uno de los tipos de runbook de hello cuatro.

Mostrar comandos de ejemplo siguiente Hola cómo toocreate un runbook nuevo vacío.

    New-AzureRmAutomationRunbook -AutomationAccountName MyAccount `
    -Name NewRunbook -ResourceGroupName MyResourceGroup -Type PowerShell

## <a name="importing-a-runbook-from-a-file-into-azure-automation"></a>Importar un runbook de un archivo en Azure Automation
Puede crear un nuevo runbook en Azure Automation importando un script de PowerShell o un flujo de trabajo de PowerShell (extensión. ps1) o un runbook gráfico exportado (.graphrunbook).  Debe especificar hello [tipo de runbook](automation-runbook-types.md) que se creará de importación de hello habida Hola de cuenta siguientes consideraciones.

* Solo se puede importar un archivo de .graphrunbook en un [runbook gráfico](automation-runbook-types.md#graphical-runbooks)nuevo y solo se pueden crear runbooks gráficos desde un archivo .graphrunbook.
* Un archivo .ps1 que contiene un flujo de trabajo de PowerShell solo se puede importar en un [runbook de flujo de trabajo de PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).  Si el archivo hello contiene varios flujos de trabajo de PowerShell, se producirá un error importación Hola. Debe guardar cada archivo propio tooits de flujo de trabajo e importar cada uno de ellos por separado.
* Un archivo .ps1 que no contenga un flujo de trabajo se puede importar en un [runbook de PowerShell](automation-runbook-types.md#powershell-runbooks) o en un [runbook de flujo de trabajo de PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).  Si se importa en un runbook de flujo de trabajo de PowerShell, entonces será convertido tooa flujo de trabajo y los comentarios se incluirán en runbook Hola especificando Hola cambios realizados.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-classic-portal"></a>tooimport un runbook desde un archivo con el portal de Azure clásico de Hola
Puede usar Hola siguiendo el procedimiento tooimport un archivo de script en la automatización de Azure.  Tenga en cuenta que solo puede importar un archivo. ps1 en un runbook de flujo de trabajo de PowerShell mediante este portal.  Debe usar hello portal de Azure para otros tipos.

1. En el portal de administración de Azure de hello, seleccione **automatización** y, a continuación, seleccione una cuenta de automatización.
2. Haga clic en **Import**.
3. Haga clic en **Buscar archivo** y busque tooimport de archivo de script de Hola.
4. Si desea tooedit Hola runbook ahora, a continuación, haga clic en **editar Runbook**. De lo contrario, haga clic en Aceptar.
5. Hola nuevo runbook aparecerá en hello **Runbooks** pestaña Hola cuenta de automatización.
6. Debe [publicar Hola runbook](#publishing-a-runbook) antes de que pueda ejecutar.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-portal"></a>tooimport un runbook desde un archivo con hello portal de Azure
Puede usar Hola siguiendo el procedimiento tooimport un archivo de script en la automatización de Azure.  

> [!NOTE]
> Tenga en cuenta que sólo se puede importar un archivo. ps1 en un runbook de flujo de trabajo de PowerShell mediante el portal de Hola.
> 
> 

1. Hola portal de Azure, abra su cuenta de automatización.
2. En hello concentrador, seleccione **Runbooks** tooopen lista de Hola de runbooks.
3. Haga clic en hello **agregar un runbook** botón y, a continuación, **importación**.
4. Haga clic en **archivo de Runbook** tooselect Hola archivo tooimport
5. Si hello **nombre** campo está habilitado, entonces tiene Hola opción toochange lo.  nombre de runbook de Hello debe empezar por una letra y puede contener letras, números, caracteres de subrayado y guiones.
6. Hola [tipo de runbook](automation-runbook-types.md) se seleccionará automáticamente, pero se puede cambiar el tipo hello después de poner restricciones aplicables de hello en cuenta. 
7. Hola nuevo runbook aparecerá en la lista Hola de runbooks para hello cuenta de automatización.
8. Debe [publicar Hola runbook](#publishing-a-runbook) antes de que pueda ejecutar.

> [!NOTE]
> Después de importar un runbook gráfico o un runbook gráfico de flujo de trabajo de PowerShell, tendrá Hola opción tooconvert toohello otro tipo si lo desea. No se puede convertir tootextual.
> 
> 

### <a name="tooimport-a-runbook-from-a-script-file-with-windows-powershell"></a>tooimport un runbook desde un archivo de script con Windows PowerShell
Puede usar hello [AzureRMAutomationRunbook de importación](https://msdn.microsoft.com/library/mt603735.aspx) cmdlet tooimport un archivo de script como un borrador de runbook de flujo de trabajo de PowerShell. Si ya existe un runbook de hello, importación de Hola se producirá un error a menos que utilice hello *-Force* parámetro. 

Hola después de comandos de ejemplo muestra cómo tooimport una secuencia de comandos de archivos en un runbook.

    $automationAccountName =  "AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"
    $RGName = "ResourceGroup"

    Import-AzureRMAutomationRunbook -Name $runbookName -Path $scriptPath `
    -ResourceGroupName $RGName -AutomationAccountName $automationAccountName `
    -Type PowerShellWorkflow 


## <a name="publishing-a-runbook"></a>Publicación de un runbook
Cuando cree o importe un runbook nuevo, debe publicarlo para poder ejecutarlo.  Cada runbook de Automation tiene una versión de borrador y una versión publicada. Versión publicada de hello solo está disponible toobe ejecutar y versión de borrador de hello solo se puede editar. versión publicada de Hola se ve afectado por cualquier versión de borrador de toohello de cambios. Cuando la versión de borrador de hello debe estar disponible, a continuación, se publica y se sobrescribe la versión publicada de hello con versión de borrador de Hola.

## <a name="toopublish-a-runbook-using-hello-azure-classic-portal"></a>toopublish un runbook mediante el portal de Azure clásico de Hola
1. Abra runbook hello en el portal de Azure clásico de Hola.
2. En la parte superior de Hola de pantalla de bienvenida, haga clic en **autor**.
3. En la parte inferior de Hola de pantalla de bienvenida, haga clic en **publicar** y, a continuación, **Sí** toohello mensaje de comprobación.

## <a name="toopublish-a-runbook-using-hello-azure-portal"></a>toopublish un runbook mediante Hola portal de Azure
1. Abra runbook Hola Hola portal de Azure.
2. Haga clic en hello **editar** botón.
3. Haga clic en hello **publicar** botón y, a continuación, **Sí** toohello mensaje de comprobación.

## <a name="toopublish-a-runbook-using-windows-powershell"></a>toopublish un runbook mediante Windows PowerShell
Puede usar hello [AzureRmAutomationRunbook publicar](https://msdn.microsoft.com/library/mt603705.aspx) cmdlet toopublish un runbook con Windows PowerShell. Mostrar comandos de ejemplo siguiente Hola cómo toopublish un runbook de ejemplo.

    $automationAccountName =  AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $RGName = "ResourceGroup"

    Publish-AzureRmAutomationRunbook -AutomationAccountName $automationAccountName `
    -Name $runbookName -ResourceGroupName $RGName


## <a name="next-steps"></a>Pasos siguientes
* toolearn acerca de cómo puede beneficiarse de hello Runbook y Galería de módulos de PowerShell, consulte [galerías de módulos y runbooks de automatización de Azure](automation-runbook-gallery.md)
* toolearn más información acerca de la edición de runbooks de flujo de trabajo de PowerShell y PowerShell con un editor de texto, consulte [edición textuales runbooks en automatización de Azure](automation-edit-textual-runbook.md)
* toolearn más información acerca de la creación de runbooks gráficos, consulte [creación gráfica en automatización de Azure](automation-graphical-authoring-intro.md)

