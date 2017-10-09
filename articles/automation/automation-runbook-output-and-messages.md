---
title: "aaaRunbook salida y mensajes en automatización de Azure | Documentos de Microsoft"
description: "Describe cómo toocreate y recuperar la salida y error de los mensajes procedentes de runbooks en automatización de Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 13a414f5-0e2c-4be2-9558-a3e3ec84b6b2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: magoedte;bwren
ms.openlocfilehash: c1505fa889473766bfa47e43aaed2449d60ad851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-output-and-messages-in-azure-automation"></a>Salidas de runbook y mensajes en la Automatización de Azure
La mayoría de los runbooks de automatización de Azure alguna forma de salida como un usuario de toohello de mensaje de error o un objeto complejo toobe consumido por otro flujo de trabajo. Windows PowerShell ofrece [varios flujos de](http://blogs.technet.com/heyscriptingguy/archive/2014/03/30/understanding-streams-redirection-and-write-host-in-powershell.aspx) toosend salida desde un script o un flujo de trabajo. Automatización de Azure funciona con cada una de estas secuencias de forma diferente, y debe seguir las prácticas recomendadas sobre cómo toouse cada cuando se crea un runbook.

Hello tabla siguiente proporciona una breve descripción de cada uno de los flujos de Hola y su comportamiento en hello Portal de administración de Azure cuando se ejecuta un runbook publicado y cuando [probar un runbook](automation-testing-runbook.md). Asimismo, en las siguientes secciones se proporciona más información sobre cada flujo.

| Stream | Description | Publicado | Prueba |
|:--- |:--- |:--- |:--- |
| Salida |Objetos destinados toobe consumido por otros runbooks. |Historial de trabajos de toohello escrito. |Se muestran en el panel de resultados de pruebas de Hola. |
| Warning (Advertencia) |Mensaje de advertencia destinado al usuario Hola. |Historial de trabajos de toohello escrito. |Se muestran en el panel de resultados de pruebas de Hola. |
| Error |Mensaje de error destinado al usuario Hola. A diferencia de una excepción, Hola runbook continúa después de un mensaje de error de forma predeterminada. |Historial de trabajos de toohello escrito. |Se muestran en el panel de resultados de pruebas de Hola. |
| Detallado |Mensajes que proporcionan información general o de depuración. |Escribir historial de toojob sólo si el registro detallado está activado para el runbook de Hola. |En el panel de resultados de pruebas de hello solo muestra si $VerbosePreference se establece tooContinue en hello runbook. |
| Progreso |Registros que se generan automáticamente antes y después de cada actividad de runbook de Hola. Hola runbook no debería intentar toocreate sus propios registros de progreso porque están dirigidos a un usuario interactivo. |Escribir historial de toojob solo si se activa el registro de progreso para el runbook de Hola. |No se muestran en el panel de resultados de pruebas de Hola. |
| Depurar |Mensajes dirigidos a un usuario interactivo. No debe usarse en runbooks. |No se escribe toojob historial. |No se escribe tooTest panel de salida. |

## <a name="output-stream"></a>Flujo de salida
flujo de salida de Hello está diseñado para la salida de los objetos creados por un script o un flujo de trabajo cuando se ejecuta correctamente. En la automatización de Azure, esta secuencia se utiliza principalmente para toobe objetos destinados consumido por [runbooks primarios que llaman runbook actual hello](automation-child-runbooks.md). Cuando se [llama a un runbook insertado](automation-child-runbooks.md#invoking-a-child-runbook-using-inline-execution) desde un runbook primario, devuelve datos de elemento primario toohello de flujo de salida de hello. Solo debe usar usuario de hello salida secuencia toocommunicate información general toohello atrás si sabe que otro runbook no llamará nunca Hola runbook. Como práctica recomendada, sin embargo, normalmente debería usar hello [flujo detallado](#Verbose) usuario toohello de toocommunicate información general.

Puede escribir el flujo de salida de toohello de datos mediante [Write-Output](http://technet.microsoft.com/library/hh849921.aspx) o colocar el objeto de hello en su propia línea hello runbook.

    #hello following lines both write an object toohello output stream.
    Write-Output –InputObject $object
    $object

### <a name="output-from-a-function"></a>Salida de una función
Cuando se escribe el flujo de salida de toohello en una función que se incluye en su runbook, resultado de hello se pasa toohello back-runbook. Si Hola runbook asigna esa variable tooa de salida, no se escribe toohello flujo de salida. Escribir tooany otro flujo desde dentro de la función hello escribirá toohello flujo correspondiente Hola runbook.

Considere la posibilidad de hello siguiente runbook de ejemplo.

    Workflow Test-Runbook
    {
        Write-Verbose "Verbose outside of function" -Verbose
        Write-Output "Output outside of function"
        $functionOutput = Test-Function
        $functionOutput

    Function Test-Function
     {
        Write-Verbose "Verbose inside of function" -Verbose
        Write-Output "Output inside of function"
      }
    }


flujo de salida de Hello trabajo del runbook Hola sería:

    Output inside of function
    Output outside of function

flujo detallado de Hello trabajo del runbook Hola sería:

    Verbose outside of function
    Verbose inside of function

Una vez haya publicado runbook hello y antes de iniciarla, también debe activar el registro en la configuración de runbook Hola Hola de tooget orden detallado transmitir el resultado detallado.

### <a name="declaring-output-data-type"></a>Declarar los tipos de datos de salida
Un flujo de trabajo puede especificar el tipo de datos de Hola de su salida mediante hello [atributo OutputType](http://technet.microsoft.com/library/hh847785.aspx). Este atributo no tiene ningún efecto en tiempo de ejecución, pero proporciona a un autor de runbook de indicación toohello en tiempo de diseño de salida de hello esperada del runbook de Hola. Como conjunto de herramientas de Hola de runbooks continúa tooevolve, aumentará la importancia de Hola de declaración de tipos de datos de salida en tiempo de diseño en importancia. Como resultado, es una práctica recomendada tooinclude esta declaración en los runbooks que cree.

Esta es una lista de tipos de salidas de ejemplo:

* System.String
* System.Int32
* System.Collections.Hashtable
* Microsoft.Azure.Commands.Compute.Models.PSVirtualMachine

Hello runbook de ejemplo siguiente genera un objeto de cadena e incluye una declaración de su tipo de salida. Si su runbook genera una matriz de un tipo determinado, todavía debe especificar tipo de hello como matriz de tooan diferencia de tipo hello.

    Workflow Test-Runbook
    {
       [OutputType([string])]

       $output = "This is some string output."
       Write-Output $output
    }

toodeclare una salida de tipo en runbooks Grapical o flujo de trabajo de PowerShell gráfica, puede seleccionar hello **de entrada y salida** opción de menú y escriba el nombre de Hola de hello tipo de salida.  Se recomienda usar toomake para nombre de clase completo .NET de Hola se puedan identificar fácilmente al hacer referencia a él desde un runbook primario.  Esto expone todas las propiedades de Hola de ese bus de datos de clase toohello runbook hello y proporciona una gran flexibilidad cuando se usen para la lógica condicional, registro y hacer referencia a como valores para otras actividades de runbook de Hola.<br> ![Opción de entrada y salida de Runbook](media/automation-runbook-output-and-messages/runbook-menu-input-and-output-option.png)

En el siguiente ejemplo de Hola, tenemos dos toodemonstrate runbooks gráficos esta característica.  Si se aplica el modelo de diseño modular runbook hello, tenemos un runbook que actúa como hello *plantilla de Runbook de autenticación* administrar la autenticación con el uso de Azure Hola cuenta de ejecución.  Nuestro segundo runbook, que normalmente realizaría Hola core lógica tooautomate un escenario que nos ocupa, en este caso va hello tooexecute *plantilla de Runbook de autenticación* y mostrar hello resultados tooyour **prueba** panel de salida.  En circunstancias normales, tendríamos que este runbook hacer algo con una salida de hello sacar provecho de recursos del runbook secundario de Hola.    

Esta es Hola lógica básica del programa Hola a **AuthenticateTo Azure** runbook.<br> ![Autenticar ejemplo de plantilla de Runbook](media/automation-runbook-output-and-messages/runbook-authentication-template.png).  

Incluye el tipo de salida de hello *Microsoft.Azure.Commands.Profile.Models.PSAzureContext*, que devuelve propiedades de perfil de autenticación de Hola.<br> ![Ejemplo de tipo de salida de Runbooks](media/automation-runbook-output-and-messages/runbook-input-and-output-add-blade.png) 

Aunque este runbook es muy sencillo, hay una toocall de elemento de configuración aquí.  Hola última actividad está ejecutando hello **Write-Output** cmdlet y escrituras Hola variable perfil datos tooa $_ mediante una expresión de PowerShell para hello **Inputobject** parámetro, que es necesario para que cmdlet.  

Hola runbook segundo en este ejemplo, denominado *ChildOutputType prueba*, simplemente tenemos dos actividades.<br> ![Runbook de tipo de salida secundario de ejemplo](media/automation-runbook-output-and-messages/runbook-display-authentication-results-example.png) 

primera actividad de Hello llama hello **AuthenticateTo Azure** hello y runbook segunda actividad ejecuta hello **Write-Verbose** cmdlet con hello **origen de datos** de  **Salida de actividad** y el valor de Hola para **ruta de acceso del campo** es **Context.Subscription.SubscriptionName**, que especifique output de contexto de Hola de hello  **Azure AuthenticateTo** runbook.<br> ![Origen de datos de parámetro del cmdlet Write-Verbose](media/automation-runbook-output-and-messages/runbook-write-verbose-parameters-config.png)    

resultado de Hello es nombre Hola de suscripción de Hola.<br> ![Resultados de Runbook de Test-ChildOutputType](media/automation-runbook-output-and-messages/runbook-test-childoutputtype-results.png)

Una nota acerca del comportamiento de Hola de hello control de tipo de salida.  Cuando se escribe un valor en el campo de tipo de salida de hello en hello entrada y la hoja de propiedades de salida, tener tooclick fuera de control de hello después de escribir, en orden para su toobe entrada reconocerlos control Hola.  

## <a name="message-streams"></a>Flujos de mensajes
A diferencia del flujo de salida de hello, flujos de mensajes son el usuario de toohello de información de toocommunicate previsto. Hay varios flujos de mensajes para los diferentes tipos de información, y Automatización de Azure controla cada uno de ellos de forma diferente.

### <a name="warning-and-error-streams"></a>Flujos de error y de advertencia
flujos de Error y advertencia de Hello son problemas de toolog previsto que se producen en un runbook. Historial de trabajos de toohello se escriben cuando se ejecuta un runbook y se incluyen en el panel de resultados de pruebas de Hola Hola Portal de administración de Azure cuando se prueba un runbook. De forma predeterminada, Hola runbook continuará ejecutándose después de un error o advertencia. Puede especificar Hola runbook debe suspenderse en una advertencia o error estableciendo un [variable de preferencia](#PreferenceVariables) Hola runbook antes de crear el mensaje de bienvenida. Por ejemplo, toocause un toosuspend runbook produce un error como lo haría una excepción, establezca **$ErrorActionPreference** tooStop.

Crear un mensaje de advertencia o error con hello [Write-Warning](https://technet.microsoft.com/library/hh849931.aspx) o [Write-Error](http://technet.microsoft.com/library/hh849962.aspx) cmdlet. Las actividades también pueden escribir secuencias de toothese.

    #hello following lines create a warning message and then an error message that will suspend hello runbook.

    $ErrorActionPreference = "Stop"
    Write-Warning –Message "This is a warning message."
    Write-Error –Message "This is an error message that will stop hello runbook because of hello preference variable."

### <a name="verbose-stream"></a>Flujo detallado
secuencia de mensajes detallados de Hello es para obtener información general sobre el funcionamiento del runbook Hola. Desde hello [flujo de depuración](#Debug) no está disponible en un runbook, deben utilizarse mensajes detallados para obtener información de depuración. De forma predeterminada, los mensajes detallados de runbooks publicados no puede almacenar en el historial de trabajos de Hola. toostore mensajes detallados, configure runbooks publicados tooLog registros detallados en pestaña configurar de Hola de runbook de Hola Hola Portal de administración de Azure. En la mayoría de los casos, debe mantener la configuración predeterminada de Hola de no escribir registros detallados para un runbook por motivos de rendimiento. Activar esta tootroubleshoot única opción o depurar un runbook.

Cuando [probar un runbook](automation-testing-runbook.md), no se muestran los mensajes detallados incluso si Hola runbook está configurado toolog de registros detallados. los mensajes detallados al toodisplay [probar un runbook](automation-testing-runbook.md), debe establecer Hola $VerbosePreference variable tooContinue. Con esa variable está establecida, los mensajes detallados se mostrará en hello panel de resultados de pruebas de hello portal de Azure.

Crear un mensaje detallado con hello [Write-Verbose](http://technet.microsoft.com/library/hh849951.aspx) cmdlet.

    #hello following line creates a verbose message.

    Write-Verbose –Message "This is a verbose message."

### <a name="debug-stream"></a>Flujo de depuración
flujo de depuración de Hello está diseñado para su uso con un usuario interactivo y no debe usarse en runbooks.

## <a name="progress-records"></a>Registros de progreso
Si configura un curso de toolog runbook registra (en la pestaña configurar de Hola de runbook de Hola Hola portal de Azure); después, un registro se escribirá toohello historial de trabajos antes y después de ejecuta cada actividad. En la mayoría de los casos, debe mantener la configuración predeterminada de Hola de no registrar registros de progreso de un runbook en el rendimiento de toomaximize de orden. Activar esta tootroubleshoot única opción o depurar un runbook. Cuando se prueba un runbook, no se muestran mensajes de progreso incluso si Hola runbook está configurado toolog registros de progreso.

Hola [Write-Progress](http://technet.microsoft.com/library/hh849902.aspx) cmdlet no es válido en un runbook porque está pensado para su uso con un usuario interactivo.

## <a name="preference-variables"></a>Variables de preferencia
Windows PowerShell usa [variables de preferencia](http://technet.microsoft.com/library/hh847796.aspx) toodetermine cómo toorespond toodata enviado toodifferent flujos de salida. Puede establecer estas variables en un toocontrol runbook cómo responderá toodata enviados a diferentes flujos.

Hello tabla siguiente enumeran las variables de preferencia de Hola que pueden usarse en runbooks con sus válido y valores predeterminados. Tenga en cuenta que esta tabla solo incluye los valores de hello que son válidos en un runbook. Valores adicionales son válidos para las variables de preferencia de hello cuando se usa en Windows PowerShell fuera de automatización de Azure.

| Variable | Valor predeterminado | Valores válidos |
|:--- |:--- |:--- |
| WarningPreference |Continuar |Stop<br>Continuar<br>SilentlyContinue |
| ErrorActionPreference |Continuar |Stop<br>Continuar<br>SilentlyContinue |
| VerbosePreference |SilentlyContinue |Stop<br>Continuar<br>SilentlyContinue |

Hello en la tabla siguiente enumera comportamiento Hola Hola valores de preferencia variable que son válidos en runbooks.

| Valor | Comportamiento |
|:--- |:--- |
| Continuar |Registra mensajes de bienvenida y continúa ejecutando el runbook de Hola. |
| SilentlyContinue |Continúa la ejecución Hola runbook sin registrar el mensaje de bienvenida. Esto tiene el efecto de Hola se pasa por alto el mensaje de bienvenida. |
| Detención |Registra mensajes de bienvenida y suspende Hola runbook. |

## <a name="retrieving-runbook-output-and-messages"></a>Recuperar salidas de runbooks y mensajes
### <a name="azure-portal"></a>Azure Portal
Puede ver detalles de Hola de un trabajo de runbook en hello portal de Azure desde la ficha trabajos del saludo de un runbook. Hola resumen del trabajo de hello mostrará los parámetros de entrada de Hola y Hola [flujo de salida](#Output) en suma toogeneral saber el trabajo de Hola y las excepciones que se hayan producido. Hola historial incluirá los mensajes de Hola [flujo de salida](#Output) y [flujos de Error y advertencia](#WarningError) en suma toohello [flujo detallado](#Verbose) y [progreso Registros](#Progress) si Hola runbook está configurado toolog detallado y registros de progreso.

### <a name="windows-powershell"></a>Windows PowerShell
En Windows PowerShell, puede recuperar mensajes de salida y de un runbook con hello [Get-AzureAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) cmdlet. Este cmdlet requiere Hola Id. de trabajo de Hola y tiene un parámetro llamado flujo donde debe especificar qué tooreturn de secuencia. Puede especificar cualquier tooreturn todos los flujos de trabajo de Hola.

Hola ejemplo siguiente inicia un runbook de ejemplo y, a continuación, espera a que se toocomplete. Una vez completado, se recopila su flujo de salida de trabajo de Hola.

    $job = Start-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook"

    $doLoop = $true
    While ($doLoop) {
       $job = Get-AzureRmAutomationJob -ResourceGroupName "ResourceGroup01" `
       –AutomationAccountName "MyAutomationAccount" -Id $job.JobId
       $status = $job.Status
       $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped")
    }

    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" -Id $job.JobId –Stream Output

### <a name="graphical-authoring"></a>Creación gráfica
Para runbooks gráficos, registro adicional está disponible en forma de Hola de seguimiento de nivel de actividad.  Hay dos niveles de seguimiento: básico y detallado.  En el seguimiento básico, puede ver Hola iniciar y tooany reintentos de actividad, como el número de intentos y la hora de inicio de actividad hello relacionados con la hora de finalización de cada actividad de runbook de hello más información.  En el seguimiento detallado, obtendrá un seguimiento básico y, además, datos de entrada y de salida para cada actividad.  Tenga en cuenta que actualmente los registros de seguimiento de Hola se escriben con flujo detallado de hello, por lo que debe habilitar el registro detallado cuando se habilita el seguimiento.  Para runbooks gráficos con el seguimiento habilitado no es necesario toolog registros de progreso, porque actúa de seguimiento básica de Hola Hola mismo propósito y es más informativo.

![Vista de secuencias de trabajos de creación de gráficos](media/automation-runbook-output-and-messages/job-streams-view-blade.png)

Puede ver de Hola por encima de la captura de pantalla que al habilitar detallado registro y seguimiento para runbooks gráficos, hay mucha más información está disponible en producción de hello que ver flujos de trabajo.  Esta información adicional puede ser esencial para solucionar problemas de producción con un Runbook. Por lo tanto, solo debería habilitarlo con este fin, y no hacerlo como regla general.    
los registros de seguimiento de Hello pueden ser especialmente numerosos.  Con un runbook gráfico seguimiento puede obtener dos registros de toofour por la actividad en función de si ha configurado el seguimiento básico o detallado.  A menos que tenga este curso de hello tootrack de información de un runbook para solucionar el problema, puede ser conveniente tookeep que seguimiento se ha desactivado.

**tooenable nivel de actividad de seguimiento, realizar Hola pasos.**

1. Hola Portal de Azure, abra su cuenta de automatización.
2. Haga clic en hello **Runbooks** icono tooopen Hola lista de runbooks.
3. En la hoja de Runbooks hello, haga clic en tooselect un runbook gráfico en la lista de runbooks.
4. En la hoja de configuración de hello runbook Hola seleccionado, haga clic en **registro y seguimiento**.
5. En hello registro y seguimiento de hoja, en registros detallados, haga clic en **en** tooenable el registro detallado y el seguimiento de nivel de actividad de udner, cambiar nivel de seguimiento de hello demasiado**básica** o **detallado**  en función de nivel de Hola de seguimiento que necesite.<br>
   
   ![Hoja de registro y seguimiento de creación de gráficos](media/automation-runbook-output-and-messages/logging-and-tracing-settings-blade.png)

### <a name="microsoft-operations-management-suite-oms-log-analytics"></a>Microsoft Operations Management Suite (OMS) Log Analytics
Automatización puede enviar runbook trabajo estado y el trabajo secuencias tooyour análisis de registros de Microsoft Operations Management Suite (OMS) área de trabajo.  Con Log Analytics puede:

* Obtener información sobre los trabajos de Automatización 
* Desencadenar un correo electrónico o una alerta en función de en el estado de trabajo del runbook (por ejemplo, error o en suspensión) 
* Escribir consultas avanzadas en las transmisiones de trabajos 
* Correlacionar trabajos en cuentas de Automatización 
* Visualizar el historial de trabajos a lo largo del tiempo    

Para obtener más información acerca de cómo tooconfigure integración con toocollect de análisis de registros, correlacionar y actuar en los datos de trabajo, consulte [reenviar el estado del trabajo y flujos de trabajo de automatización tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).

## <a name="next-steps"></a>Pasos siguientes
* más información acerca de la ejecución de un runbook, cómo toomonitor runbook trabajos y otros detalles técnicos, consulte toolearn [realizar un seguimiento de un trabajo de runbook](automation-runbook-execution.md)
* toounderstand toodesign y usar runbooks secundarios, vea [runbooks secundarios en automatización de Azure](automation-child-runbooks.md)

