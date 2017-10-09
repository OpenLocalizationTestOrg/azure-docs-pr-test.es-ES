---
title: "aaaChild runbooks en automatización de Azure | Documentos de Microsoft"
description: "Describe las diferentes maneras de hello para iniciar un runbook en automatización de Azure desde otro runbook y compartir información entre ellos."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 919887b9-43e2-4c16-883c-f81807fe37db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d3d06818d344b565d53cc4f4705b41dcfcf9a376
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="child-runbooks-in-azure-automation"></a>Runbooks secundarios en la Automatización de Azure
Es un procedimiento recomendado en automatización de Azure toowrite runbooks reutilizables, modulares, con una función independiente que se puede usar por otros runbooks. Un runbook primario a menudo llamará a uno o varios runbooks secundarios tooperform requerido funcionalidad. Hay dos toocall formas un runbook secundario, y cada una presenta diferencias que debe conocer para que pueda determinar cuál es la mejor para los diferentes escenarios.

## <a name="invoking-a-child-runbook-using-inline-execution"></a>Invocación de un runbook secundario mediante la ejecución en línea
tooinvoke un runbook insertado desde otro runbook, utilice Hola nombre de runbook de Hola y proporcione valores para sus parámetros exactamente igual que haría una actividad o un cmdlet.  Hola a todos los runbooks en la misma cuenta de automatización es tooall disponible otros toobe usadas de esta manera. Hola el runbook primario esperará Hola secundarios runbook toocomplete antes de mover la línea siguiente toohello y se devuelve ningún resultado directamente toohello primario.

Cuando se invoca un runbook insertado, se ejecuta en hello mismo trabajo como Hola el runbook primario. No habrá ninguna indicación en el historial de trabajos de hello del runbook secundario de Hola que se ejecutó. Las excepciones y las salidas del runbook secundario de hello flujos se asociarán con primario Hola. Esto da como resultado menos trabajos y facilita tootrack y tootroubleshoot desde cualquier excepción producida por el runbook secundario hello y cualquiera de sus resultados de la secuencia se asocian de trabajo primario de Hola.

Cuando se publica un runbook, cualquier runbook secundario al que llame deberá estar ya estar publicado. Esto es así porque la Automatización de Azure crea una asociación con los runbooks secundarios cuando se compila un runbook. Si no, el runbook primario Hola aparecerá toopublish correctamente, pero generará una excepción cuando se inicie. Si esto ocurre, puede volver a publicar el runbook primario de hello en orden tooproperly referencia Hola secundarios runbooks. No es necesario toorepublish Hola primario runbook si se cambia cualquiera de los runbooks secundarios Hola porque ya se habrá creado Hola asociación.

parámetros de Hola de un runbook secundario llamado en línea pueden ser cualquier tipo de datos, incluidos objetos complejos y no hay ningún [serialización JSON](automation-starting-a-runbook.md#runbook-parameters) como al iniciar runbook hello mediante Hola Portal de administración de Azure o con hello Cmdlet de inicio AzureRmAutomationRunbook.

### <a name="runbook-types"></a>Tipos de runbook
Qué tipos pueden llamarse entre sí:

* Un [runbook de PowerShell](automation-runbook-types.md#powershell-runbooks) y los [runbooks gráficos](automation-runbook-types.md#graphical-runbooks) pueden llamarse entre sí en línea (ambos se basan en PowerShell).
* Un [runbook de flujo de trabajo de PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) y los runbooks gráficos de flujo de trabajo de PowerShell pueden llamarse entre sí en línea (ambos tipos se basan en el flujo de trabajo de PowerShell).
* tipos de PowerShell de Hola y Hola que tipos de flujo de trabajo de PowerShell no puede llamar a alineadas entre sí y debe utilizar AzureRmAutomationRunbook de inicio.

Cuándo es importante el orden de publicación:

* Hola publicar runbooks solo es importante orden de runbooks de flujo de trabajo de PowerShell y flujo de trabajo de PowerShell gráfica.

Cuando se llama a un runbook secundario gráficos o flujo de trabajo de PowerShell con una ejecución en línea, usa solo Hola de runbook de Hola.  Cuando se llama a un runbook secundario de PowerShell, debe precedido a su nombre *.\\*  toospecify que hello secuencia de comandos se encuentra en el directorio local de Hola. 

### <a name="example"></a>Ejemplo
Hola siguiente ejemplo, invoca un runbook secundario de prueba que acepta tres parámetros, un objeto complejo, un entero y un valor booleano. salida de Hello de hello el runbook secundario se asigna tooa variable.  En este caso, el runbook secundario hello es un runbook de flujo de trabajo de PowerShell

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = PSWF-ChildRunbook –VM $vm –RepeatCount 2 –Restart $true

Aquí te mostramos Hola mismo ejemplo con un runbook de PowerShell como elemento secundario de Hola.

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = .\PS-ChildRunbook.ps1 –VM $vm –RepeatCount 2 –Restart $true


## <a name="starting-a-child-runbook-using-cmdlet"></a>Inicio de un runbook secundario mediante un cmdlet
Puede usar hello [inicio AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart cmdlet un runbook tal como se describe en [toostart un runbook con Windows PowerShell](automation-starting-a-runbook.md#starting-a-runbook-with-windows-powershell). Existen dos modos de usar este cmdlet.  En un modo Hola cmdlet devuelve Id. de trabajo de hello en cuanto se crea el trabajo de secundarios de hello runbook secundario se Hola.  En Hola otro modo, que se habilita mediante la especificación de hello **-espere** parámetro, el cmdlet de hello esperará hasta secundarios Hola trabajo finaliza y devolverá la salida de hello del runbook secundario de Hola.

trabajo de Hola de un runbook secundario iniciado con un cmdlet se ejecutará en un trabajo independiente desde el runbook primario Hola. Esto da como resultado el número de trabajos que cuando se invoca Hola runbook insertado y hace más difícil tootrack. primario Hola puede iniciar varios runbooks secundarios de forma asincrónica sin tener que esperar cada toocomplete. Para ese mismo tipo de ejecución en paralelo al llamar a runbooks secundarios de hello en línea, Hola el runbook primario necesitaría hello toouse [palabra clave parallel](automation-powershell-workflow.md#parallel-processing).

Los parámetros de un runbook secundario iniciado con un cmdlet se proporcionan como una tabla hash, tal y como se describe en [Parámetros de runbook](automation-starting-a-runbook.md#runbook-parameters). Solo pueden usarse los tipos de datos simples. Si runbook hello tiene un parámetro con un tipo de datos complejos, a continuación, debe llamarse en línea.

### <a name="example"></a>Ejemplo
Hello en el ejemplo siguiente se inicia un runbook secundario con parámetros y, a continuación, espera a que se toocomplete con hello AzureRmAutomationRunbook inicio-espera el parámetro. Una vez completado, se recopila su salida del runbook secundario de Hola.

    $params = @{"VMName"="MyVM";"RepeatCount"=2;"Restart"=$true} 
    $joboutput = Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-ChildRunbook" -ResourceGroupName "LabRG" –Parameters $params –wait


## <a name="comparison-of-methods-for-calling-a-child-runbook"></a>Comparación de métodos para llamar a un runbook secundario
Hello siguiente tabla resume las diferencias de hello entre dos métodos de Hola para llamar a un runbook desde otro runbook.

|  | En línea | Cmdlet |
|:--- |:--- |:--- |
| Trabajo |Runbooks secundarios se ejecutan en hello mismo trabajo como elemento primario de Hola. |Se crea un trabajo independiente para el runbook secundario Hola. |
| Ejecución |El runbook primario espera Hola secundarios runbook toocomplete antes de continuar. |El runbook primario continúa inmediatamente después de que se inicie el runbook secundario *o* runbook primario espera Hola secundarios trabajo toofinish. |
| Salida |El runbook primario puede obtener los resultados directamente del runbook secundario. |El runbook primario debe obtener los resultados directamente del trabajo de runbook secundario *o* el runbook primario puede obtener los resultados directamente del runbook secundario. |
| parameters |Valores de parámetros del runbook secundario Hola se especifican por separado y pueden usar cualquier tipo de datos. |Valores de hello secundarios runbook parámetros deben combinarse en una sola tabla hash y solo pueden incluir el simple, de matriz y tipos de datos que utilicen la serialización JSON de objeto. |
| Cuenta de automatización |El runbook primario solo puede usar runbook secundario Hola misma cuenta de automatización. |El runbook primario puede usar runbook secundario desde cualquier cuenta de automatización de hello misma suscripción de Azure e incluso de otra suscripción si tiene una tooit de conexión. |
| Publicación |El runbook secundario debe publicarse antes de publicar el runbook primario. |El runbook secundario debe publicarse en cualquier momento antes de iniciar el runbook primario. |

## <a name="next-steps"></a>Pasos siguientes
* [Inicio de un runbook en Automatización de Azure](automation-starting-a-runbook.md)
* [Salidas de runbook y mensajes en la Automatización de Azure](automation-runbook-output-and-messages.md)

