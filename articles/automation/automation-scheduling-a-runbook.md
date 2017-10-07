---
title: "aaaScheduling un runbook en automatización de Azure | Documentos de Microsoft"
description: "Describe cómo toocreate una programación en automatización de Azure para que puede iniciar automáticamente un runbook en un momento determinado o según una programación periódica."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 710979ff-99d8-41e4-ac6d-6bf26b8ea654
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/09/2016
ms.author: bwren
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: c215b7ff6aa200466f3be566facba3c0cffcc924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Programación de un runbook en Automatización de Azure
tooschedule un runbook en automatización de Azure toostart en un momento determinado, vincúlelo tooone o más programaciones. Una programación puede ser configurado tooeither ejecutarse una vez o de forma recurrente programada cada hora o diariamente para runbooks de hello portal de Azure clásico y para runbooks de hello portal de Azure, puede además programarlas para días semanales, mensuales, específicos de la semana de Hola o los días de mes de Hello, o un día concreto del mes de Hola.  Un runbook puede estar vinculado toomultiple programaciones y una programación puede tener varios tooit runbooks vinculados.

## <a name="creating-a-schedule"></a>Creación de una programación
Puede crear una nueva programación de runbooks en hello portal de Azure, en el portal clásico de hello, o con Windows PowerShell. También tiene opción de Hola de creación de una nueva programación al vincular una programación de tooa runbook mediante hello Azure clásico o el portal de Azure.

> [!NOTE]
> Al asociar una programación a un runbook, automatización almacena hello las versiones actuales de los módulos de hello en su cuenta y vínculos de programación de toothat.  Esto significa que si tenía un módulo con la versión 1.0 en su cuenta cuando se creó una programación y, a continuación, actualizar Hola módulo tooversion 2.0, programación de hello seguirán toouse 1.0.  En la versión actualizada del módulo de orden toouse hello, debe crear una nueva programación. 
> 
> 

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a>toocreate una nueva programación Hola portal de Azure clásico
1. Hola portal de Azure clásico, seleccione automatización y, a continuación, seleccione nombre de Hola de una cuenta de automatización.
2. Seleccione hello **activos** ficha.
3. En la parte inferior de Hola de ventana hello, haga clic en **Agregar configuración**.
4. Haga clic en **Agregar programación**.
5. Escriba un **nombre** y, opcionalmente, un **descripción** para schedule.your nueva Hola se ejecutará la programación **una vez**, **por hora**, **Diaria**, **semanal**, o **mensual**.
6. Especifique un **Start Time** y otras opciones en función de tipo hello de programación que seleccionó.

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a>toocreate una nueva programación Hola portal de Azure
1. Hola portal de Azure, desde su cuenta de automatización, haga clic en hello **activos** icono tooopen hello **activos** hoja.
2. Haga clic en hello **programaciones** icono tooopen hello **programaciones** hoja.
3. Haga clic en **agregar una programación** princip Hola de hoja de Hola.
4. En hello **nueva programación** hoja, escriba un **nombre** y, opcionalmente, un **descripción** de nueva programación de Hola.
5. Seleccione si la programación de Hola se ejecutará una vez o según una programación recurrente seleccionando **una vez** o **periodicidad**.  Si selecciona **Una vez**, especifique una hora en **Hora de inicio** y haga clic en **Crear**.  Si selecciona **periodicidad**, especifique un **hora de inicio** y la frecuencia de hello para la frecuencia con desea Hola runbook toorepeat - por **hora**, **día**, **semana**, o por **mes**.  Si selecciona **semana** o **mes** de lista desplegable de hello, Hola **opción de periodicidad** aparecerá en la hoja de Hola y tras la selección, hello **periodicidad opción** hoja se mostrará y se puede seleccionar día Hola de semana si seleccionó **semana**.  Si seleccionó **mes**, puedes elegir por **días de la semana** o días específicos del mes de hello en Hola calendario y por último, desea toorun en Hola último día del mes de Hola o no y, a continuación, haga clic en **Aceptar** .   

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a>toocreate una nueva programación con Windows PowerShell
Puede usar hello [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) toocreate cmdlet una nueva programación de automatización de Azure para runbooks clásicos, o [AzureRmAutomationSchedule New](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet para runbooks de hello Azure Portal. Debe especificar la hora de inicio de Hola de programación de Hola y la frecuencia de hello debe ejecutarse.

Hola después de comandos de ejemplo muestra cómo toocreate una nueva programación que ejecuta cada día a las 3:30 P.M. a partir de 20 de enero de 2015 de un cmdlet de administración de servicios de Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

Hello en el ejemplo siguiente comandos muestra cómo toocreate una programación para hello 15 y 30 de cada mes con un cmdlet de Azure Resource Manager.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-tooa-runbook"></a>Vincular un runbook de tooa de programación
Un runbook puede estar vinculado toomultiple programaciones y una programación puede tener varios tooit runbooks vinculados. Si un runbook tiene parámetros, puede proporcionar valores para ellos. Debe proporcionar valores para los parámetros obligatorios y puede proporcionar valores para los parámetros opcionales.  Estos valores se utilizarán cada vez que se inicia Hola runbook por esta programación.  Puede adjuntar Hola misma runbook tooanother programación y especificar distintos valores de parámetros.

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a>toolink un runbook de tooa de programación con hello portal de Azure clásico
1. Hola portal de Azure clásico, seleccione **automatización** y, a continuación, haga clic en nombre de Hola de una cuenta de automatización.
2. Seleccione hello **Runbooks** ficha.
3. Haga clic en el nombre de Hola de hello runbook tooschedule.
4. Haga clic en hello **programación** ficha.
5. Si Hola runbook no está vinculado actualmente tooa programación, se le ofrecerá la opción de hello demasiado**vincular tooa nueva programación** o **vincular tooan programación existente**.  Si Hola runbook está vinculado actualmente tooa programación, haga clic en **vínculo** en Hola parte inferior de hello ventana tooaccess estas opciones.
6. Si Hola runbook tiene parámetros, se le pedirá sus valores.  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a>toolink un runbook de tooa de programación con hello portal de Azure
1. Hola portal de Azure, desde su cuenta de automatización, haga clic en hello **Runbooks** icono tooopen hello **Runbooks** hoja.
2. Haga clic en el nombre de Hola de hello runbook tooschedule.
3. Si Hola runbook no está vinculado actualmente tooa programación, a continuación, se le Hola determinada opción toocreate una programación nueva o vincular tooan existente de la programación.  
4. Si Hola runbook tiene parámetros, puede seleccionar opción de hello **modificar la configuración de ejecución (valor predeterminado: Azure)** hello y **parámetros** hoja se muestra donde se pueda escribir información de hello en consecuencia.  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a>toolink un runbook de tooa de programación con Windows PowerShell
Puede usar hello [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink un runbook clásico de programación tooa o [AzureRmAutomationScheduledRunbook Register](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet para runbooks de hello portal de Azure.  Puede especificar valores para parámetros del runbook Hola con parámetros de Hola. Consulte [Inicio de un runbook en Automatización de Azure](automation-starting-a-runbook.md) para obtener más información sobre cómo especificar valores de parámetro.

Mostrar comandos de ejemplo siguiente Hola cómo toolink una programación con un cmdlet de administración de servicios de Azure con parámetros.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

Mostrar comandos de ejemplo siguiente Hola cómo toolink un runbook de tooa de programación con un cmdlet de Azure Resource Manager con parámetros.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a>Deshabilitación de una programación
Cuando se deshabilita una programación, cualquier tooit runbooks vinculados ya no se ejecutarán según dicha programación. Puede deshabilitar una programación manualmente o establecer una fecha de expiración para las programaciones con frecuencia al crearlas. Cuando se alcanza la fecha de expiración de hello, se deshabilitará la programación de Hola.

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a>toodisable una programación de hello portal de Azure clásico
Puede deshabilitar una programación en el portal de Azure clásico de página de detalles de la programación de Hola de programación de Hola Hola.

1. Hola portal de Azure clásico, seleccione automatización y, a continuación, haga clic en nombre de Hola de una cuenta de automatización.
2. Seleccione la ficha de activos de Hola.
3. Haga clic en nombre de Hola de una programación tooopen la página de detalles.
4. Cambio **habilitado** demasiado**No**.

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a>toodisable una programación de hello portal de Azure
1. Hola portal de Azure, desde su cuenta de automatización, haga clic en hello **activos** icono tooopen hello **activos** hoja.
2. Haga clic en hello **programaciones** icono tooopen hello **programaciones** hoja.
3. Haga clic en el nombre de Hola de una hoja de detalles de programación tooopen Hola.
4. Cambio **habilitado** demasiado**No**.

### <a name="toodisable-a-schedule-with-windows-powershell"></a>toodisable una programación con Windows PowerShell
Puede usar hello [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) propiedades de hello toochange de cmdlet de una programación existente para un runbook clásico o [AzureRmAutomationSchedule conjunto](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet para runbooks de hello Azure Portal. Hola toodisable programar, especifique **false** para hello **IsEnabled** parámetro.

Hola después de comandos de ejemplo muestra cómo toodisable una programación utilizando Hola cmdlet de administración de servicios de Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

Mostrar comandos de ejemplo siguiente Hola cómo toodisable una programación para un runbook con un cmdlet de Azure Resource Manager.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a>Pasos siguientes
* toolearn más acerca de cómo trabajar con una programación, vea [activos de programación de automatización de Azure](http://msdn.microsoft.com/library/azure/dn940016.aspx)
* tooget a trabajar con runbooks en automatización de Azure, consulte [a partir de un Runbook en automatización de Azure](automation-starting-a-runbook.md) 

