---
title: "aaaLearning flujo de trabajo de PowerShell para la automatización de Azure | Documentos de Microsoft"
description: "Este artículo está pensado como una lección rápida para los autores familiarizados con PowerShell toounderstand hello las diferencias específicas entre PowerShell y flujo de trabajo de PowerShell y runbooks de conceptos tooAutomation aplicables."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 84bf133e-5343-4e0e-8d6c-bb14304a70db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 362c504eb96d31b99a826b128e6a591beecaa084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a>Aprendizaje de los conceptos básicos del flujo de trabajo de Windows PowerShell para los runbooks de Automation 
Los runbooks de Azure Automation se implementan como flujos de trabajo de Windows PowerShell.  Un flujo de trabajo de Windows PowerShell es el script de Windows PowerShell tooa similar pero presenta algunas diferencias importantes que pueden ser confusos tooa nuevo usuario.  Aunque este artículo está previsto toohelp escribir runbooks mediante el flujo de trabajo de PowerShell, se recomienda que escribir runbooks con PowerShell, a menos que tenga puntos de control.  Hay varias diferencias de sintaxis al crear runbooks de flujo de trabajo de PowerShell y estas diferencias requieren un poco más trabajo toowrite efectivo los flujos de trabajo.  

Un flujo de trabajo es una secuencia de pasos conectados y programados que realizan tareas de larga duración o requieren la coordinación de Hola de varios pasos en varios dispositivos o nodos administrados. ventajas de un flujo de trabajo en un script normal Hello incluyen capacidad de hello toosimultaneously realizar una acción en varios dispositivos y Hola capacidad tooautomatically recuperarse de errores. Un flujo de trabajo de Windows PowerShell es un script de Windows PowerShell que usa Windows Workflow Foundation. Mientras el flujo de trabajo de Hola se escribe con sintaxis de Windows PowerShell y se inicia mediante Windows PowerShell, se procesa mediante Windows Workflow Foundation.

Para obtener información detallada sobre los temas de hello en este artículo, consulte [Introducción a Workflow de Windows PowerShell](http://technet.microsoft.com/library/jj134242.aspx).

## <a name="basic-structure-of-a-workflow"></a>Estructura básica de un flujo de trabajo
Hello primer paso tooconverting un flujo de trabajo de PowerShell de PowerShell script tooa incluye con hello **flujo de trabajo** palabra clave.  Inicia un flujo de trabajo con hello **flujo de trabajo** palabra clave seguida de cuerpo de Hola de script de Hola encerrado entre llaves. nombre de Hola de flujo de trabajo de hello sigue hello **flujo de trabajo** palabra clave tal y como se muestra en hello según la sintaxis:

    Workflow Test-Workflow
    {
       <Commands>
    }

Hola nombre de flujo de trabajo de hello debe coincidir con hello de runbook de automatización de Hola. Si se va a importar runbook hello, Hola filename debe coincidir con el nombre de flujo de trabajo de Hola y debe terminar en *. ps1*.

flujo de trabajo de tooadd parámetros toohello, use hello **Param** palabra clave como lo haría con script tooa.

## <a name="code-changes"></a>Cambios de código
Código de flujo de trabajo de PowerShell examina el código de script de tooPowerShell casi idéntico salvo algunos cambios importantes.  Hola siguientes secciones describe los cambios que necesite toomake tooa PowerShell script para toorun en un flujo de trabajo.

### <a name="activities"></a>Actividades
Una actividad es una tarea específica de un flujo de trabajo. Al igual que un script se compone de uno o varios comandos, un flujo de trabajo se compone de una o varias actividades que se realizan en secuencia. Flujo de trabajo de Windows PowerShell convierte automáticamente muchos de hello tooactivities de cmdlets de Windows PowerShell cuando se ejecuta un flujo de trabajo. Cuando se especifica uno de estos cmdlets en su runbook, actividad de hello correspondiente se ejecuta mediante Windows Workflow Foundation. Para los cmdlets sin una actividad correspondiente, el flujo de trabajo de Windows PowerShell ejecuta automáticamente Hola cmdlet dentro de un [InlineScript](#inlinescript) actividad. Hay un conjunto de cmdlets que están excluidos y no se pueden usar en un flujo de trabajo a menos que incluya explícitamente en un bloque de InlineScript. Para obtener más información sobre estos conceptos, consulte [Uso de actividades en los flujos de trabajo de scripts](http://technet.microsoft.com/library/jj574194.aspx).

Las actividades de flujo de trabajo comparten un conjunto de tooconfigure de parámetros comunes su funcionamiento. Para obtener más información acerca de los parámetros comunes de flujo de trabajo de hello, consulte [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).

### <a name="positional-parameters"></a>Parámetros posicionales
No puede usar parámetros posicionales con actividades y cmdlets en un flujo de trabajo.  Todo esto significa que debe usar nombres de parámetros.

Por ejemplo, considere la posibilidad de hello después el código que obtiene todos los servicios en ejecución.

     Get-Service | Where-Object {$_.Status -eq "Running"}

Si intentas toorun este mismo código en un flujo de trabajo, recibirá un mensaje como "Parámetro de conjunto no se puede resolver con hello especificado denominado parámetros".  toocorrect, proporcionar nombre del parámetro hello como en el siguiente Hola.

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a>Objetos deserializados
Los objetos de los flujos de trabajo están deserializados.  Esto significa que sus propiedades siguen estando disponibles, pero no sus métodos.  Por ejemplo, considere la posibilidad de hello siguiente código de PowerShell que se detiene un servicio mediante el método de Stop Hola Hola de objeto de servicio.

    $Service = Get-Service -Name MyService
    $Service.Stop()

Si intentas toorun esto en un flujo de trabajo, recibirá un error que indica que "no es posible invocar métodos en un flujo de trabajo de Windows PowerShell."  

Una opción es toowrap estas dos líneas de código en un [InlineScript](#inlinescript) bloquear en cuyo caso $Service sería un objeto de servicio dentro de bloques de Hola.

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

Otra opción es toouse Hola a otro cmdlet que realiza la misma funcionalidad que el método de hello, si está disponible.  En nuestro ejemplo, el cmdlet de hello Stop-Service proporciona Hola misma funcionalidad que el método de detención de hello y podría utilizar siguiente Hola para un flujo de trabajo.

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a>InlineScript
Hola **InlineScript** actividad es útil cuando necesita uno o más comandos de toorun como tradicional script de PowerShell en lugar de flujo de trabajo de PowerShell.  Mientras que los comandos en un flujo de trabajo se envían tooWindows Workflow Foundation para su procesamiento, comandos de un bloque de InlineScript se procesan mediante Windows PowerShell.

InlineScript usa Hola sintaxis que se muestra a continuación.

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

Puede devolver resultados desde un InlineScript mediante la asignación de variable de tooa de salida de hello. Hello en el ejemplo siguiente se detiene un servicio y, a continuación, genera el nombre del servicio de Hola.

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


Puede pasar valores en un bloque de InlineScript, pero debe usar el modificador de ámbito **$Using** .  Hello en el ejemplo siguiente se es idéntico toohello ejemplo anterior salvo que hello nombre de servicio proporciona una variable.

    Workflow Stop-MyService
    {
        $ServiceName = "MyService"

        $Output = InlineScript {
            $Service = Get-Service -Name $Using:ServiceName
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


Aunque las actividades de InlineScript pueden resultar fundamental en ciertos flujos de trabajo, no se son compatibles con construcciones de flujo de trabajo y sólo debe utilizarse cuando sea necesario para hello siguientes motivos:

* No puede usar [puntos de comprobación](#checkpoints) dentro de un bloque de InlineScript. Si se produce un error en el bloque de hello, se debe reanudar desde principio Hola del bloque de Hola.
* No puede usar la [ejecución en paralelo](#parallel-processing) dentro de un bloque de InlineScript.
* InlineScript afecta a la escalabilidad de flujo de trabajo de hello ya que retiene la sesión de Windows PowerShell de hello hasta alcanzar la longitud completa Hola del bloque de InlineScript Hola.

Para más información sobre el uso de InlineScript, vea [Ejecutar comandos de Windows PowerShell en un flujo de trabajo](http://technet.microsoft.com/library/jj574197.aspx) y [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).

## <a name="parallel-processing"></a>Procesamiento en paralelo
Una ventaja de flujos de trabajo de Windows PowerShell es Hola capacidad tooperform un conjunto de comandos en paralelo en lugar de secuencialmente como con un script típico.

Puede usar hello **paralelo** palabra clave toocreate un bloque de script con varios comandos que se ejecutan simultáneamente. Esto utiliza Hola sintaxis que se muestra a continuación. En este caso, Activity1 y Activity2 se inicia en hello mismo tiempo. Activity3 se inicia después de que se hayan completado Activity1 y Activity2.

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


Por ejemplo, considere la posibilidad de hello siga los comandos de PowerShell que varios archivos tooa red destino de la copia.  Estos comandos se ejecutan secuencialmente para que un archivo debe finalizar copia antes de Hola a continuación se inicia.     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

Hello siguiente flujo de trabajo ejecuta estos mismos comandos en paralelo para que todos ellos comenzarán a copiar Hola mismo tiempo.  Solo después de que todos estén copiados se mensaje de bienvenida de finalización muestra.

    Workflow Copy-Files
    {
        Parallel
        {
            Copy-Item -Path "C:\LocalPath\File1.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File2.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File3.txt" -Destination "\\NetworkPath"
        }

        Write-Output "Files copied."
    }


Puede usar hello **ForEach-Parallel** construir comandos tooprocess para cada elemento de una colección simultáneamente. elementos de Hola de colección de Hola se procesan en paralelo mientras comandos Hola Hola bloque de script se ejecutan secuencialmente. Esto utiliza Hola sintaxis que se muestra a continuación. En este caso, Activity1 se inicia en hello la misma hora para todos los elementos de la colección de Hola. Para cada elemento, Activity2 se inicia una vez completado Activity1. Activity3 se inicia únicamente después de que se hayan completado Activity1 y Activity2 para todos los elementos.

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

Hola siguiente ejemplo es similar toohello de ejemplo anterior copiar archivos en paralelo.  En este caso, se muestra un mensaje para cada archivo después de copiarse.  Solo después de que todos estén completamente copiados se mensajes de bienvenida del final de conclusión muestra.

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach -Parallel ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
        }

        Write-Output "All files copied."
    }

> [!NOTE]
> No se recomienda ejecutando runbooks secundarios en paralelo, ya que esto ha demostrado toogive de resultados no confiables.  Hello salida del runbook a veces de hello secundario no se muestra, y puede afectar la configuración en un elemento secundario runbook Hola otros runbooks secundarios paralelas
>

## <a name="checkpoints"></a>Puntos de control
A *punto de comprobación* es una instantánea del estado actual de Hola de flujo de trabajo de Hola que incluye el valor actual de Hola para las variables y los resultados se punto toothat generado. Si un flujo de trabajo termina en error o está suspendido, Hola próxima vez que se ejecute se iniciará desde su último punto de comprobación en lugar de inicio de Hola de flujo de trabajo de Hola.  Puede establecer un punto de control en un flujo de trabajo con hello **Checkpoint-Workflow** actividad.

En el siguiente código de ejemplo de Hola, se produce una excepción después de Activity2 que produce Hola tooend de flujo de trabajo. Cuando se vuelve a ejecutar el flujo de trabajo de hello, se inicia ejecutando Activity2, ya que se encontraba justo detrás de hello último punto de control establecido.

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

Debe establecer los puntos de comprobación en un flujo de trabajo después de que las actividades que pueden ser propensas a tooexception y no deben repiten si se reanuda el flujo de trabajo de Hola. Por ejemplo, el flujo de trabajo puede crear una máquina virtual. Puede establecer un punto de control antes y después de la máquina virtual de hello comandos toocreate Hola. Si se produce un error en la creación de hello, se repetiría comandos Hola si se inicia el flujo de trabajo de Hola de nuevo. Si se produce un error en el flujo de trabajo de hello después Hola se crea correctamente, a continuación, máquina virtual de hello no se creará nuevo cuando se reanuda el flujo de trabajo de Hola.

Hola siguiente ejemplo copia la ubicación de red de varios archivos tooa y establece un punto de control después de cada archivo.  Si se pierde la ubicación de red de hello, flujo de trabajo de hello termina en error.  Cuando se inicia de nuevo, se reanudará en hello último punto de comprobación lo que significa que sólo los archivos de Hola que ya se han copiado se omiten.

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
            Checkpoint-Workflow
        }

        Write-Output "All files copied."
    }

Puesto que las credenciales de nombre de usuario no se conservan después de llamar a hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) actividad o después de hello último punto de comprobación, necesita tooset Hola credenciales toonull y, a continuación, recuperarlos nuevo desde el almacén de activos de hello después  **Flujo de trabajo suspender** o se denomina punto de comprobación.  En caso contrario, recibirá Hola siguiente mensaje de error: *no se puede reanudar el flujo de trabajo de hello, ya sea porque los datos de persistencia no se pudieron guardar por completo, o guardar datos de persistencia se ha dañado. Debe reiniciar el flujo de trabajo de Hola.*

Hola siguiendo el mismo código se muestra cómo toohandle esto en sus runbooks de flujo de trabajo de PowerShell.

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first toocreate hello VM (code not shown)

          # Now add hello VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


Este paso no es necesario si se autentica utilizando una cuenta de ejecución configurada con una entidad de servicio.  

Para obtener más información acerca de los puntos de control, vea [tooa de puntos de control Agregar flujo de trabajo de Script](http://technet.microsoft.com/library/jj574114.aspx).

## <a name="next-steps"></a>Pasos siguientes
* tooget a trabajar con runbooks de flujo de trabajo de PowerShell, consulte [mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md)
