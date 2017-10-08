---
title: "aaaSchedules en automatización de Azure | Documentos de Microsoft"
description: "Las programaciones de automatización son tooschedule usa runbooks en automatización de Azure toostart automáticamente. Describe cómo toocreate y administrar una programación de modo que puede iniciar automáticamente un runbook en un momento determinado o según una programación periódica."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1c2da639-ad20-4848-920b-88e471b2e1d9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2016
ms.author: magoedte
ms.openlocfilehash: 888a5d15fd3442a2b8ab18dd8b0eb4ab9ad0c0d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Programación de un runbook en Automatización de Azure
tooschedule un runbook en automatización de Azure toostart en un momento determinado, vincúlelo tooone o más programaciones. Una programación puede ser configurado tooeither ejecutar una sola vez o cada hora una vuelva a ocurrir o programación diaria de runbooks en el portal de Azure clásico de Hola y de runbooks en hello portal de Azure, también puede programar ellos durante días semanales, mensuales, específicos de la semana de Hola o días de hello mes, o un día concreto del mes de Hola.  Un runbook puede estar vinculado toomultiple programaciones y una programación puede tener varios tooit runbooks vinculados.

> [!NOTE]
> Las programaciones no admiten actualmente las configuraciones de DSC de Automatización de Azure.
> 
> 

## <a name="windows-powershell-cmdlets"></a>Cmdlets de Windows PowerShell
cmdlets de Hello en hello en la tabla siguiente son toocreate usado y administrar programaciones con Windows PowerShell en automatización de Azure. Se incluyen como parte del programa Hola a [módulo Azure PowerShell](/powershell/azure/overview).

| Cmdlets | Descripción |
|:--- |:--- |
| **Cmdlets de Azure Resource Manager** | |
| [Get-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/get-azurermautomationschedule) |Recupera una programación. |
| [New-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) |Crea una nueva programación. |
| [Remove-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/remove-azurermautomationschedule) |Quita una programación. |
| [Set-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) |Establece las propiedades de Hola de una programación existente. |
| [Get-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/set-azurermautomationscheduledrunbook) |Recupera runbooks programados. |
| [Register-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) |Asocia un runbook con una programación. |
| [Unregister-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/unregister-azurermautomationscheduledrunbook) |Anula la asociación de un runbook con una programación. |
| **Cmdlets de administración de servicios de Azure** | |
| [Get-AzureAutomationSchedule](/powershell/module/azure/get-azureautomationschedule?view=azuresmps-3.7.0) |Recupera una programación. |
| [New-AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) |Crea una nueva programación. |
| [Remove-AzureAutomationSchedule](/powershell/module/azure/remove-azureautomationschedule?view=azuresmps-3.7.0) |Quita una programación. |
| [Set-AzureAutomationSchedule](/powershell/module/azure/set-azureautomationschedule?view=azuresmps-3.7.0) |Establece las propiedades de Hola de una programación existente. |
| [Get-AzureAutomationScheduledRunbook](/powershell/module/azure/get-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Recupera runbooks programados. |
| [Register-AzureAutomationScheduledRunbook](/powershell/module/azure/register-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Asocia un runbook con una programación. |
| [Unregister-AzureAutomationScheduledRunbook](/powershell/module/azure/unregister-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Anula la asociación de un runbook con una programación. |

## <a name="creating-a-schedule"></a>Creación de una programación
Puede crear una nueva programación de runbooks en hello portal de Azure, en el portal clásico de hello, o con Windows PowerShell. También tiene opción de Hola de creación de una nueva programación al vincular una programación de tooa runbook mediante hello Azure clásico o el portal de Azure.

> [!NOTE]
> Automatización de Azure utilizará módulos más recientes de hello en su cuenta de automatización cuando se ejecuta un nuevo trabajo programado.  tooavoid que afectan a los runbooks y Hola procesos automatizan, primero debe probar los runbooks que vinculó programaciones con una cuenta de automatización dedicada para realizar pruebas.  Esto validará programados runbooks siguen toowork correctamente y si no es así, puede solucionar problemas y aplicar los cambios necesarios antes de migrar Hola actualizado runbook versión tooproduction.  
>  La cuenta de automatización no obtendrá automáticamente las nuevas versiones de módulos, a menos que se haya actualizado manualmente seleccionando hello [módulos de Azure Update](automation-update-azure-modules.md) opción de hello **módulos** hoja. 
>  

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a>toocreate una nueva programación Hola portal de Azure
1. Hola portal de Azure, desde su cuenta de automatización, haga clic en hello **activos** icono tooopen hello **activos** hoja.
2. Haga clic en hello **programaciones** icono tooopen hello **programaciones** hoja.
3. Haga clic en **agregar una programación** princip Hola de hoja de Hola.
4. En hello **nueva programación** hoja, escriba un **nombre** y, opcionalmente, un **descripción** de nueva programación de Hola.
5. Seleccione si la programación de Hola se ejecutará una vez o según una programación recurrente seleccionando **una vez** o **periodicidad**.  Si selecciona **Una vez**, especifique una hora en **Hora de inicio** y haga clic en **Crear**.  Si selecciona **periodicidad**, especifique un **hora de inicio** y la frecuencia de hello para la frecuencia con desea Hola runbook toorepeat - por **hora**, **día**, **semana**, o por **mes**.  Si selecciona **semana** o **mes** de lista desplegable de hello, Hola **opción de periodicidad** aparecerá en la hoja de Hola y tras la selección, hello **periodicidad opción** hoja se mostrará y se puede seleccionar día Hola de semana si seleccionó **semana**.  Si seleccionó **mes**, puedes elegir por **días laborables** o días específicos del mes de hello en Hola calendario y por último, desea toorun en Hola último día del mes de Hola o no y, a continuación, haga clic en **Aceptar** .   

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a>toocreate una nueva programación Hola portal de Azure clásico
1. Hola portal de Azure clásico, seleccione automatización y, a continuación, seleccione nombre de Hola de una cuenta de automatización.
2. Seleccione hello **activos** ficha.
3. En la parte inferior de Hola de ventana hello, haga clic en **Agregar configuración**.
4. Haga clic en **Agregar programación**.
5. Escriba un **nombre** y, opcionalmente, un **descripción** para schedule.your nueva Hola se ejecutará la programación **una vez**, **por hora**, **Diaria**, **semanal**, o **mensual**.
6. Especifique un **Start Time** y otras opciones en función de tipo hello de programación que seleccionó.

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a>toocreate una nueva programación con Windows PowerShell
Puede usar hello [New-AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) toocreate cmdlet una nueva programación de automatización de Azure para runbooks clásicos, o [AzureRmAutomationSchedule New](/powershell/module/azurerm.automation/new-azurermautomationschedule) cmdlet para runbooks de hello Azure Portal. Debe especificar la hora de inicio de Hola de programación de Hola y la frecuencia de hello debe ejecutarse.

Mostrar comandos de ejemplo siguiente Hola cómo toocreate una programación para hello 15 y 30 de cada mes con un cmdlet de Azure Resource Manager.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"

Hola después de comandos de ejemplo muestra cómo toocreate una nueva programación que ejecuta cada día a las 3:30 P.M. a partir de 20 de enero de 2015 de un cmdlet de administración de servicios de Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

## <a name="linking-a-schedule-tooa-runbook"></a>Vincular un runbook de tooa de programación
Un runbook puede estar vinculado toomultiple programaciones y una programación puede tener varios tooit runbooks vinculados. Si un runbook tiene parámetros, puede proporcionar valores para ellos. Debe proporcionar valores para los parámetros obligatorios y puede proporcionar valores para los parámetros opcionales.  Estos valores se utilizarán cada vez que se inicia Hola runbook por esta programación.  Puede adjuntar Hola misma runbook tooanother programación y especificar distintos valores de parámetros.

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a>toolink un runbook de tooa de programación con hello portal de Azure
1. Hola portal de Azure, desde su cuenta de automatización, haga clic en hello **Runbooks** icono tooopen hello **Runbooks** hoja.
2. Haga clic en el nombre de Hola de hello runbook tooschedule.
3. Si Hola runbook no está vinculado actualmente tooa programación, a continuación, se le Hola determinada opción toocreate una programación nueva o vincular tooan existente de la programación.  
4. Si Hola runbook tiene parámetros, puede seleccionar opción de hello **modificar la configuración de ejecución (valor predeterminado: Azure)** hello y **parámetros** hoja se muestra donde se pueda escribir información de hello en consecuencia.  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a>toolink un runbook de tooa de programación con hello portal de Azure clásico
1. Hola portal de Azure clásico, seleccione **automatización** y, a continuación, haga clic en nombre de Hola de una cuenta de automatización.
2. Seleccione hello **Runbooks** ficha.
3. Haga clic en el nombre de Hola de hello runbook tooschedule.
4. Haga clic en hello **programación** ficha.
5. Si Hola runbook no está vinculado actualmente tooa programación, se le ofrecerá la opción de hello demasiado**vincular tooa nueva programación** o **vincular tooan programación existente**.  Si Hola runbook está vinculado actualmente tooa programación, haga clic en **vínculo** en Hola parte inferior de hello ventana tooaccess estas opciones.
6. Si Hola runbook tiene parámetros, se le pedirá sus valores.  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a>toolink un runbook de tooa de programación con Windows PowerShell
Puede usar hello [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink un runbook clásico de programación tooa o [AzureRmAutomationScheduledRunbook Register](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) cmdlet para runbooks de hello portal de Azure.  Puede especificar valores para parámetros del runbook Hola con parámetros de Hola. Consulte [Inicio de un runbook en Automatización de Azure](automation-starting-a-runbook.md) para obtener más información sobre cómo especificar valores de parámetro.

Mostrar comandos de ejemplo siguiente Hola cómo toolink un runbook de tooa de programación con un cmdlet de Azure Resource Manager con parámetros.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"
Mostrar comandos de ejemplo siguiente Hola cómo toolink una programación con un cmdlet de administración de servicios de Azure con parámetros.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

## <a name="disabling-a-schedule"></a>Deshabilitación de una programación
Cuando se deshabilita una programación, cualquier tooit runbooks vinculados ya no se ejecutarán según dicha programación. Puede deshabilitar una programación manualmente o establecer una fecha de expiración para las programaciones con frecuencia al crearlas. Cuando se alcanza la fecha de expiración de hello, se deshabilitará la programación de Hola.

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a>toodisable una programación de hello portal de Azure
1. Hola portal de Azure, desde su cuenta de automatización, haga clic en hello **activos** icono tooopen hello **activos** hoja.
2. Haga clic en hello **programaciones** icono tooopen hello **programaciones** hoja.
3. Haga clic en el nombre de Hola de una hoja de detalles de programación tooopen Hola.
4. Cambio **habilitado** demasiado**No**.

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a>toodisable una programación de hello portal de Azure clásico
Puede deshabilitar una programación en el portal de Azure clásico de página de detalles de la programación de Hola de programación de Hola Hola.

1. Hola portal de Azure clásico, seleccione automatización y, a continuación, haga clic en nombre de Hola de una cuenta de automatización.
2. Seleccione la ficha de activos de Hola.
3. Haga clic en nombre de Hola de una programación tooopen la página de detalles.
4. Cambio **habilitado** demasiado**No**.

### <a name="toodisable-a-schedule-with-windows-powershell"></a>toodisable una programación con Windows PowerShell
Puede usar hello [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) propiedades de hello toochange de cmdlet de una programación existente para un runbook clásico o [AzureRmAutomationSchedule conjunto](/powershell/module/azurerm.automation/set-azurermautomationschedule) cmdlet para runbooks de hello Azure Portal. Hola toodisable programar, especifique **false** para hello **IsEnabled** parámetro.

Mostrar comandos de ejemplo siguiente Hola cómo toodisable una programación para un runbook con un cmdlet de Azure Resource Manager.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"

Hola después de comandos de ejemplo muestra cómo toodisable una programación utilizando Hola cmdlet de administración de servicios de Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

## <a name="next-steps"></a>Pasos siguientes
* tooget a trabajar con runbooks en automatización de Azure, consulte [a partir de un Runbook en automatización de Azure](automation-starting-a-runbook.md) 

