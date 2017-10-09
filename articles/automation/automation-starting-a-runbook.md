---
title: "aaaStarting un runbook en automatización de Azure | Documentos de Microsoft"
description: "Resume Hola diferentes métodos pueden ser utilizado toostart un runbook en automatización de Azure y proporciona detalles sobre el uso de ambos Hola portal de Azure y Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: e44bce5b56b8e803f9247fbb4f3d4db7ab35c913
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a>Inicio de un runbook en Azure Automation
Hello en la tabla siguiente le ayudará a determinar Hola método toostart un runbook en automatización de Azure que es más adecuado tooyour escenario en particular. Este artículo incluye detalles acerca de cómo iniciar un runbook con hello portal de Azure y con Windows PowerShell. Detalles de Hola se proporcionan otros métodos en otra documentación que puede tener acceso desde los siguientes vínculos de Hola.

| **MÉTODO** | **CARACTERÍSTICAS** |
| --- | --- |
| [Azure Portal](#starting-a-runbook-with-the-azure-portal) |<li>Método más sencillo con la interfaz de usuario interactiva.<br> <li>Valores de parámetro simples de tooprovide de formulario.<br> <li>Seguimiento sencillo del estado del trabajo.<br> <li>Acceso autenticado con inicio de sesión de Azure. |
| [Windows PowerShell](https://msdn.microsoft.com/library/dn690259.aspx) |<li>Permite llamar desde la línea de comandos con los cmdlets de Windows PowerShell.<br> <li>Puede incluirse en una solución automatizada con varios pasos.<br> <li>La solicitud se autentica con el certificado o el usuario de OAuth principal/servicio principal.<br> <li>Permite proporcionar valores de parámetro simples y complejos.<br> <li>Realizar el seguimiento del estado del trabajo.<br> <li>Cmdlets de PowerShell de toosupport necesario de cliente. |
| [API de Automatización de Azure](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li>El método más flexible, pero también más complejo.<br> <li>Permite llamar desde cualquier código personalizado que pueda realizar solicitudes HTTP.<br> <li>La solicitud se autentica con el certificado o el usuario de OAuth principal/servicio principal.<br> <li>Permite proporcionar valores de parámetro simples y complejos.<br> <li>Realizar el seguimiento del estado del trabajo. |
| [Webhooks](automation-webhooks.md) |<li>Permite iniciar el runbook desde una única solicitud HTTP.<br> <li>Autenticado con el token de seguridad de la dirección URL.<br> <li>Cliente no puede invalidar los valores de parámetro especificados al crear webhook. Runbook puede definir un parámetro único que se rellena con los detalles de la solicitud HTTP Hola.<br> <li>Ningún estado de trabajo de capacidad tootrack a través de la dirección URL del webhook. |
| [Responder tooAzure alerta](../log-analytics/log-analytics-alerts.md) |<li>Iniciar un runbook de alerta de tooAzure de respuesta.<br> <li>Configurar webhook para el runbook y vincular tooalert.<br> <li>Autenticado con el token de seguridad de la dirección URL. |
| [Programación](automation-schedules.md) |<li>Permite iniciar automáticamente el runbook en una programación según la hora, diaria, semanal o mensual.<br> <li>Permite manipular la programación a través de Azure Portal, los cmdlets de PowerShell o la API de Azure.<br> <li>Proporcionar toobe de valores de parámetro utilizado con la programación. |
| [Desde otro Runbook](automation-child-runbooks.md) |<li>Permite usar un runbook como una actividad en otro runbook.<br> <li>Es útil para la funcionalidad utilizada por varios runbooks.<br> <li>Proporcionar runbook de toochild de valores de parámetro y utilice la salida en el runbook primario. |

Hello siguiente imagen ilustra proceso paso a paso detallado Hola ciclo de vida de un runbook. Incluye maneras diferentes que se inicia un runbook en automatización de Azure, los componentes necesarios para runbooks de automatización de Azure tooexecute Hybrid Runbook Worker y las interacciones entre distintos componentes. toolearn acerca de cómo ejecutar runbooks de automatización en su centro de datos, consulte demasiado[hybrid runbook Worker](automation-hybrid-runbook-worker.md)

![Arquitectura de runbook](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a>A partir de un runbook Hola portal de Azure
1. Hola portal de Azure, seleccione **automatización** y, a continuación, haga clic en nombre de Hola de una cuenta de automatización.
2. En el menú del concentrador hello, seleccione **Runbooks**.
3. En hello **Runbooks** hoja, seleccione un runbook y, a continuación, haga clic en **iniciar**.
4. Si Hola runbook tiene parámetros, es posible que tooprovide solicitadas valores con un cuadro de texto para cada parámetro. Consulte [Parámetros de runbook](#Runbook-parameters) a continuación para obtener más información sobre los parámetros.
5. En hello **trabajo** hoja, puede ver estado de Hola de trabajo de runbook de Hola.

## <a name="starting-a-runbook-with-windows-powershell"></a>Inicio de un runbook con Windows PowerShell
Puede usar hello [AzureRmAutomationRunbook inicio](https://msdn.microsoft.com/library/mt603661.aspx) toostart un runbook con Windows PowerShell. Hello código de ejemplo siguiente inicia un runbook denominado Test-Runbook.

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

Inicio AzureRmAutomationRunbook devuelve un trabajo de un objeto que se puede usar tootrack su estado una vez que se inicie el runbook de Hola. A continuación, puede utilizar este objeto de trabajo con [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine estado de Hola de trabajo de Hola y [AzureRmAutomationJobOutput Get](https://msdn.microsoft.com/library/mt603476.aspx) tooget su salida. Hola siguiendo el ejemplo de código inicia un runbook denominado Test-Runbook, espera hasta que se ha completado y, a continuación, muestra su salida.

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

Si Hola runbook requiere parámetros, debe proporcionarlos como una [hashtable](http://technet.microsoft.com/library/hh847780.aspx) donde clave Hola de tabla hash de hello coincide con el nombre del parámetro de Hola y el valor de hello es el valor del parámetro de Hola. Hello en el ejemplo siguiente se muestra cómo toostart un runbook con dos parámetros de cadena denominado FirstName y LastName, un número entero denominado RepeatCount y un parámetro booleano denominado Show. Para obtener información adicional sobre los parámetros, consulte [Parámetros de runbook](#Runbook-parameters) a continuación.

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a>Parámetros de runbook
Cuando se inicia un runbook desde Hola Portal de Azure o Windows PowerShell, instrucción de Hola se envía a través de hello servicio web automatización de Azure. Este servicio no admite parámetros con tipos de datos complejos. Si necesita tooprovide un valor para un parámetro complejo, debe llamarlo en línea desde otro runbook como se describe en [runbooks secundarios en automatización de Azure](automation-child-runbooks.md).

Hola servicio web automatización de Azure proporcionará funciones especiales para los parámetros mediante ciertos tipos de datos como se describe en las secciones siguientes de Hola.

### <a name="named-values"></a>Valores con nombre
Si parámetro hello es el tipo de datos [objeto], puede usar Hola después toosend de formato JSON, una lista de valores con nombre: *{nombre1: 'Value1', nombre2: 'Valor2', Nombre3: 'Value3'}*. Estos valores deben ser tipos simples. Hola runbook recibirá el parámetro hello como un [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) con propiedades que corresponden a tooeach con el nombre value.

Considere la posibilidad de hello siguiente runbook de prueba que acepta un parámetro denominado usuario.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

Hello texto siguiente podría utilizarse para el parámetro de usuario de Hola.

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

Esto da como resultado Hola después de salida.

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a>Matrices
Si el parámetro hello es una matriz, como [matriz] o [cadena []], puede usar Hola siguientes toosend de formato JSON, una lista de valores: *[valor1, valor2, Valor3]*. Estos valores deben ser tipos simples.

Considere la posibilidad de hello siguiente runbook de prueba que acepta un parámetro denominado *usuario*.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

Hello texto siguiente podría utilizarse para el parámetro de usuario de Hola.

```
["Joe","Smith",2,true]
```

Esto da como resultado Hola después de salida.

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a>Credenciales
Si el parámetro hello es el tipo de datos **PSCredential**, puede proporcionar el nombre de Hola de una automatización de Azure [activo de credencial](automation-credentials.md). Hola runbook recuperará la credencial de hello con nombre de Hola que especifique.

Considere la posibilidad de hello siguiente runbook de prueba que acepta un parámetro denominado credencial.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

Hello texto siguiente podría utilizarse para el parámetro de usuario de hello suponiendo que hubiese un activo de credencial denominado *Mi credencial*.

```
My Credential
```

Si es que Hola username de credencial de hello *jsmith*, esto da como resultado Hola después de salida.

```
jsmith
```

## <a name="next-steps"></a>Pasos siguientes
* arquitectura de runbook de Hello en el artículo actual proporciona una descripción general de administración de recursos de runbooks en Azure y locales con hello Hybrid Runbook Worker.  toolearn acerca de cómo ejecutar runbooks de automatización en su centro de datos, consulte demasiado[Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).
* toolearn más información acerca de hello crear toobe runbooks modulares utilizada por otros runbooks para funciones específicas o comunes, consulte demasiado[Runbooks secundarios](automation-child-runbooks.md).

