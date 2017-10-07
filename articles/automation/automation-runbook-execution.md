---
title: "ejecución de aaaRunbook en automatización de Azure | Documentos de Microsoft"
description: "Describe los detalles de Hola de cómo se procesa un runbook en automatización de Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d10c8ce2-2c0b-4ea7-ba3c-d20e09b2c9ca
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: bwren
ms.openlocfilehash: bdb535675443353d44640bc7773de3f9dac5e42c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-execution-in-azure-automation"></a>Ejecución de un runbook en Automatización de Azure
Cuando se inicia un runbook en Automatización de Azure, se crea un trabajo. Un trabajo es una instancia única de ejecución de un runbook. Una automatización de Azure trabajador está asignado toorun cada trabajo. Aunque los trabajadores se comparten por varias cuentas de Azure, los trabajos de diferentes cuentas de Automatización están aislados entre sí. No tiene control sobre qué solicitud de hello de servicios de trabajo para su trabajo.  Un único runbook puede tener varios trabajos que se ejecutan al mismo tiempo. Al ver lista de Hola de runbooks en hello portal de Azure, muestra el estado de Hola de todos los trabajos que se iniciaron para cada runbook. Puede ver lista de Hola de trabajos para cada runbook en estado de hello tootrack los pedidos de cada uno. Para obtener una descripción de hello diferentes Estados de trabajo, consulte [Estados de trabajo](#job-statuses).

Hello siguiente diagrama muestra hello del ciclo de vida de un trabajo de runbook para [runbooks gráficos](automation-runbook-types.md#graphical-runbooks) y [runbooks de flujo de trabajo de PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).

![Estados de trabajo: flujo de trabajo de PowerShell](./media/automation-runbook-execution/job-statuses.png)

Hello siguiente diagrama muestra hello del ciclo de vida de un trabajo de runbook para [runbooks PowerShell](automation-runbook-types.md#powershell-runbooks).

![Estados de trabajo: script de PowerShell](./media/automation-runbook-execution/job-statuses-script.png)

Los trabajos tienen acceso tooyour Azure recursos mediante la realización de una suscripción de Azure tooyour de conexión. Solo tienen acceso tooresources en su centro de datos si esos recursos son accesibles desde la nube pública de Hola.

## <a name="job-statuses"></a>Estados del trabajo
Hello siguiente tabla describe Hola diferentes estados posibles de un trabajo.

| Estado | Descripción |
|:--- |:--- |
| Completed |ha completado correctamente el trabajo de Hola. |
| Con error |Para [runbooks gráficos y flujo de trabajo de PowerShell](automation-runbook-types.md), error del runbook de hello toocompile.  Para [runbooks de Script de PowerShell](automation-runbook-types.md), error del runbook de hello toostart u Hola trabajo detecta una excepción. |
| Error, esperando recursos |Error del trabajo de Hello porque ha alcanzado hello [equilibrada](#fairshare) limitar tres veces e iniciarse desde Hola mismo punto de control o desde Hola iniciar de hello runbook cada vez. |
| En cola |Hola trabajo está esperando recursos en un toocome de trabajo de automatización disponible para que se puede iniciar. |
| Iniciando |trabajo de Hola se ha asignado el trabajo tooa y sistema Hola está en proceso de Hola de iniciarlo. |
| Reanudando |sistema de Hello está en proceso de Hola de reanudar el trabajo de hello después de haberse suspendido. |
| En ejecución |trabajo de saludo se está ejecutando. |
| En ejecución, esperando recursos |Hello trabajo se ha descargado porque ha alcanzado hello [equilibrada](#fairshare) límite. Se reanuda en breve desde su último punto de control. |
| Stopped |se detuvo el trabajo de Hola por usuario de hello antes de completarse. |
| Deteniéndose |sistema de Hello está en proceso de Hola de detener el trabajo de Hola. |
| Suspended |Hola trabajo se suspendió usuario hello, sistema de Hola o un comando hello runbook. Un trabajo que está suspendido se puede iniciar de nuevo y se reanudará desde su último punto de control o desde el principio de Hola de hello runbook si no tiene puntos de control. sistema de hello solo suspenderá Hola runbook cuando se produce una excepción. De forma predeterminada, se establece demasiado ErrorActionPreference**continuar**, lo que significa que el trabajo de hello sigue ejecutándose en un error. Si esta variable de preferencia se establece demasiado**detener**, a continuación, se suspende el trabajo de hello en un error.  Se aplica demasiado[runbooks gráficos y flujo de trabajo de PowerShell](automation-runbook-types.md) solo. |
| Suspendiendo |sistema de Hello intenta realizar trabajo de hello toosuspend a la solicitud de saludo del usuario de Hola. Hola runbook debe alcanzar el punto de control siguiente antes de que se pueda suspender. Si ya ha pasado su último punto de control, se completa antes de que se pueda suspender.  Se aplica demasiado[runbooks gráficos y flujo de trabajo de PowerShell](automation-runbook-types.md) solo. |

## <a name="viewing-job-status-from-hello-azure-portal"></a>Ver el estado del trabajo de hello portal de Azure
Puede ver un resumen de estado de todos los trabajos de runbook o profundizar en los detalles de un trabajo de runbook específico en hello portal de Azure o mediante la configuración de integración con el estado del trabajo de runbook de análisis de registros de Microsoft Operations Management Suite (OMS) área de trabajo tooforward y flujos de trabajo.  Para obtener más información sobre la integración con análisis de registros de OMS, consulte [reenviar el estado del trabajo y flujos de trabajo de automatización tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).  

### <a name="automation-runbook-jobs-summary"></a>Resumen de trabajos de runbook de Automation
En hello derecha de la cuenta de automatización seleccionada, puede ver un resumen de todos los trabajos de runbook de Hola para una cuenta de automatización seleccionada en **estadísticas trabajos** icono.<br><br> ![Icono Estadísticas de trabajo](./media/automation-runbook-execution/automation-account-job-status-summary.png).<br> Este icono muestra un recuento y una representación gráfica del estado del trabajo de Hola para todos los trabajos que se ejecuta.  

Al hacer clic en el icono de hello presenta hello **trabajos** hoja, que incluye una lista resumida de todos los trabajos que se ejecuta, con el estado, la ejecución del trabajo y horas de inicio y finalización.<br><br> ![Hoja Trabajos de cuenta de Automation](./media/automation-runbook-execution/automation-account-jobs-status-blade.png)<br><br>  Puede filtrar lista Hola de trabajos seleccionando **filtre los trabajos** y filtrar en un runbook específico, el estado del trabajo o de lista desplegable de hello, Hola toosearch de intervalo de fecha y hora en.<br><br> ![Filtrar estado del trabajo](./media/automation-runbook-execution/automation-account-jobs-filter.png)

Como alternativa, puede ver detalles de resumen de trabajo para un runbook específico seleccionando dicho runbook de hello **Runbooks** hoja en tu cuenta de automatización y, a continuación, seleccione Hola **trabajos** icono.  Esto presenta hello **trabajos** hoja, y desde allí puede hacer clic en tooview de registro de trabajo de hello sus detalles y el resultado.<br><br> ![Hoja Trabajos de cuenta de Automation](./media/automation-runbook-execution/automation-runbook-job-summary-blade.png)<br> 

### <a name="job-summary"></a>Resumen del trabajo
Puede ver una lista de todos los trabajos de Hola que se han creado para un runbook determinado y su estado más reciente. Puede filtrar la lista por el estado del trabajo y Hola intervalo de fechas para saludo del último cambio toohello trabajo. tooview su información detallada y salida, haga clic en nombre de Hola de un trabajo. Hello vista detallada del trabajo de hello incluye valores de hello para parámetros de runbook de Hola que se proporcionaron toothat trabajo.

Puede usar Hola siguiendo los pasos tooview Hola de trabajos de un runbook.

1. Hola portal de Azure, seleccione **automatización** y, a continuación, seleccione nombre de Hola de una cuenta de automatización.
2. Desde el concentrador de hello, seleccione **Runbooks** y, a continuación, en hello **Runbooks** hoja seleccionar un runbook de lista Hola.
3. En hoja Hola runbook Hola seleccionado, haga clic en hello **trabajos** icono.
4. Haga clic en uno de los trabajos de hello en lista de Hola y de hoja de detalles de trabajo de runbook de hello puede ver sus detalles y el resultado.

## <a name="retrieving-job-status-using-windows-powershell"></a>Recuperación del estado del trabajo con Windows PowerShell
Puede usar hello [AzureRmAutomationJob Get](https://msdn.microsoft.com/library/mt619440.aspx) trabajos de hello tooretrieve creados para un runbook y Hola los detalles de un trabajo determinado. Si se inicia un runbook con Windows PowerShell mediante [AzureRmAutomationRunbook inicio](https://msdn.microsoft.com/library/mt603661.aspx), a continuación, devuelve el trabajo resultante Hola. Use [Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx)tooget de salida de salida de un trabajo.

Hello comandos de ejemplo siguientes recuperar el último trabajo de un runbook de muestra de Hola y muestra su estado, los valores de hello proporcionados para los parámetros de runbook de Hola y Hola de salida de trabajo de Hola.

    $job = (Get-AzureRmAutomationJob –AutomationAccountName "MyAutomationAccount" `
    –RunbookName "Test-Runbook" -ResourceGroupName "ResourceGroup01" | sort LastModifiedDate –desc)[0]
    $job.Status
    $job.JobParameters
    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAcct" -Id $job.JobId –Stream Output

## <a name="fair-share"></a>distribución equilibrada
En los recursos de tooshare de orden entre todos los runbooks en la nube de hello, automatización de Azure descargará temporalmente cualquier trabajo después de que se ha estado ejecutando durante tres horas.  Durante este tiempo, los trabajos de [runbooks basados en PowerShell](automation-runbook-types.md#powershell-runbooks) se detienen y no se reiniciarán.  Hola muestra de estado de trabajo **detenido**.  Este tipo de runbook siempre se reinicia desde el principio de hello, ya que no admiten los puntos de control.  

Los [runbooks basados en el flujo de trabajo de PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) se reanudarán a partir de su último [punto de control](https://docs.microsoft.com/system-center/sma/overview-powershell-workflows#bk_Checkpoints).  Después de ejecutar tres horas, se suspenderá el trabajo del runbook de Hola por el servicio de Hola y su estado se muestra **ejecutando, esperando recursos**.  Cuando hay disponible un espacio aislado, Hola runbook se reiniciará automáticamente por el servicio de automatización de Hola y se reanuda desde el último punto de comprobación Hola.  Este es el comportamiento normal del flujo de trabajo de PowerShell a la hora de suspender o reiniciar.  Si Hola runbook nuevo superior a tres horas de tiempo de ejecución, se repite el proceso de hello, toothree horas.  Después de hello reiniciarse por tercera vez, si Hola runbook todavía no se ha completado en tres horas, a continuación, es Error del trabajo de runbook de Hola y muestra el estado del trabajo de hello **error, esperando recursos**.  En este caso, recibirá Hola tras excepción con un error de Hola.

*trabajo Hola no puede continuar ejecutándose porque se expulsó repetidamente desde Hola mismo punto de control. Asegúrese de que el runbook no realiza operaciones largas sin conservar su estado.*

Éste es el servicio de Hola de tooprotect de ejecución de runbooks indefinidamente sin completar, ya que no son toomake pueda lo toohello siguiente punto de control sin que se descargue de nuevo.

Si runbook hello no tiene ningún punto de control o trabajo de hello no había alcanzado el primer punto de control hello antes de descargarse, reinicia desde el principio de Hola.  

Cuando se crea un runbook, debe asegurarse de que toorun de tiempo de hello las actividades entre dos puntos de control no supere los tres horas. Puede que necesite tooadd puntos de comprobación tooyour runbook tooensure que no alcanza este límite de tres horas o dividir larga ejecución de las operaciones. Por ejemplo, su runbook podría realizar una reindexación en una gran base de datos SQL. Si no lleva a cabo esta operación solo en Hola razonable límite de recurso compartido y, a continuación, el trabajo de Hola se descarga y se reinician desde el principio de Hola. En este caso, debe interrumpir la operación de reindización de hello en varios pasos, como reindizar una tabla a la vez y, a continuación, inserte un punto de control después de cada operación de modo que hello trabajo se pudiera reanudar después de hello última operación toocomplete.

## <a name="next-steps"></a>Pasos siguientes
* toolearn más información acerca de métodos diferentes de Hola que pueden ser utilizado toostart un runbook en automatización de Azure, consulte [a partir de un runbook en automatización de Azure](automation-starting-a-runbook.md)

