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
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="9db1a-103">Inicio de un runbook en Azure Automation</span><span class="sxs-lookup"><span data-stu-id="9db1a-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="9db1a-104">Hello en la tabla siguiente le ayudará a determinar Hola método toostart un runbook en automatización de Azure que es más adecuado tooyour escenario en particular.</span><span class="sxs-lookup"><span data-stu-id="9db1a-104">hello following table will help you determine hello method toostart a runbook in Azure Automation that is most suitable tooyour particular scenario.</span></span> <span data-ttu-id="9db1a-105">Este artículo incluye detalles acerca de cómo iniciar un runbook con hello portal de Azure y con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9db1a-105">This article includes details on starting a runbook with hello Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="9db1a-106">Detalles de Hola se proporcionan otros métodos en otra documentación que puede tener acceso desde los siguientes vínculos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9db1a-106">Details on hello other methods are provided in other documentation that you can access from hello links below.</span></span>

| <span data-ttu-id="9db1a-107">**MÉTODO**</span><span class="sxs-lookup"><span data-stu-id="9db1a-107">**METHOD**</span></span> | <span data-ttu-id="9db1a-108">**CARACTERÍSTICAS**</span><span class="sxs-lookup"><span data-stu-id="9db1a-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="9db1a-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9db1a-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="9db1a-110">Método más sencillo con la interfaz de usuario interactiva.</span><span class="sxs-lookup"><span data-stu-id="9db1a-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="9db1a-111">Valores de parámetro simples de tooprovide de formulario.</span><span class="sxs-lookup"><span data-stu-id="9db1a-111">Form tooprovide simple parameter values.</span></span><br> <li><span data-ttu-id="9db1a-112">Seguimiento sencillo del estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="9db1a-112">Easily track job state.</span></span><br> <li><span data-ttu-id="9db1a-113">Acceso autenticado con inicio de sesión de Azure.</span><span class="sxs-lookup"><span data-stu-id="9db1a-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="9db1a-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="9db1a-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="9db1a-115">Permite llamar desde la línea de comandos con los cmdlets de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9db1a-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="9db1a-116">Puede incluirse en una solución automatizada con varios pasos.</span><span class="sxs-lookup"><span data-stu-id="9db1a-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="9db1a-117">La solicitud se autentica con el certificado o el usuario de OAuth principal/servicio principal.</span><span class="sxs-lookup"><span data-stu-id="9db1a-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="9db1a-118">Permite proporcionar valores de parámetro simples y complejos.</span><span class="sxs-lookup"><span data-stu-id="9db1a-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="9db1a-119">Realizar el seguimiento del estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="9db1a-119">Track job state.</span></span><br> <li><span data-ttu-id="9db1a-120">Cmdlets de PowerShell de toosupport necesario de cliente.</span><span class="sxs-lookup"><span data-stu-id="9db1a-120">Client required toosupport PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="9db1a-121">API de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="9db1a-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="9db1a-122">El método más flexible, pero también más complejo.</span><span class="sxs-lookup"><span data-stu-id="9db1a-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="9db1a-123">Permite llamar desde cualquier código personalizado que pueda realizar solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="9db1a-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="9db1a-124">La solicitud se autentica con el certificado o el usuario de OAuth principal/servicio principal.</span><span class="sxs-lookup"><span data-stu-id="9db1a-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="9db1a-125">Permite proporcionar valores de parámetro simples y complejos.</span><span class="sxs-lookup"><span data-stu-id="9db1a-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="9db1a-126">Realizar el seguimiento del estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="9db1a-126">Track job state.</span></span> |
| [<span data-ttu-id="9db1a-127">Webhooks</span><span class="sxs-lookup"><span data-stu-id="9db1a-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="9db1a-128">Permite iniciar el runbook desde una única solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="9db1a-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="9db1a-129">Autenticado con el token de seguridad de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="9db1a-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="9db1a-130">Cliente no puede invalidar los valores de parámetro especificados al crear webhook.</span><span class="sxs-lookup"><span data-stu-id="9db1a-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="9db1a-131">Runbook puede definir un parámetro único que se rellena con los detalles de la solicitud HTTP Hola.</span><span class="sxs-lookup"><span data-stu-id="9db1a-131">Runbook can define single parameter that is populated with hello HTTP request details.</span></span><br> <li><span data-ttu-id="9db1a-132">Ningún estado de trabajo de capacidad tootrack a través de la dirección URL del webhook.</span><span class="sxs-lookup"><span data-stu-id="9db1a-132">No ability tootrack job state through webhook URL.</span></span> |
| [<span data-ttu-id="9db1a-133">Responder tooAzure alerta</span><span class="sxs-lookup"><span data-stu-id="9db1a-133">Respond tooAzure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="9db1a-134">Iniciar un runbook de alerta de tooAzure de respuesta.</span><span class="sxs-lookup"><span data-stu-id="9db1a-134">Start a runbook in response tooAzure alert.</span></span><br> <li><span data-ttu-id="9db1a-135">Configurar webhook para el runbook y vincular tooalert.</span><span class="sxs-lookup"><span data-stu-id="9db1a-135">Configure webhook for runbook and link tooalert.</span></span><br> <li><span data-ttu-id="9db1a-136">Autenticado con el token de seguridad de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="9db1a-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="9db1a-137">Programación</span><span class="sxs-lookup"><span data-stu-id="9db1a-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="9db1a-138">Permite iniciar automáticamente el runbook en una programación según la hora, diaria, semanal o mensual.</span><span class="sxs-lookup"><span data-stu-id="9db1a-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="9db1a-139">Permite manipular la programación a través de Azure Portal, los cmdlets de PowerShell o la API de Azure.</span><span class="sxs-lookup"><span data-stu-id="9db1a-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="9db1a-140">Proporcionar toobe de valores de parámetro utilizado con la programación.</span><span class="sxs-lookup"><span data-stu-id="9db1a-140">Provide parameter values toobe used with schedule.</span></span> |
| [<span data-ttu-id="9db1a-141">Desde otro Runbook</span><span class="sxs-lookup"><span data-stu-id="9db1a-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="9db1a-142">Permite usar un runbook como una actividad en otro runbook.</span><span class="sxs-lookup"><span data-stu-id="9db1a-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="9db1a-143">Es útil para la funcionalidad utilizada por varios runbooks.</span><span class="sxs-lookup"><span data-stu-id="9db1a-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="9db1a-144">Proporcionar runbook de toochild de valores de parámetro y utilice la salida en el runbook primario.</span><span class="sxs-lookup"><span data-stu-id="9db1a-144">Provide parameter values toochild runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="9db1a-145">Hello siguiente imagen ilustra proceso paso a paso detallado Hola ciclo de vida de un runbook.</span><span class="sxs-lookup"><span data-stu-id="9db1a-145">hello following image illustrates detailed step-by-step process in hello life cycle of a runbook.</span></span> <span data-ttu-id="9db1a-146">Incluye maneras diferentes que se inicia un runbook en automatización de Azure, los componentes necesarios para runbooks de automatización de Azure tooexecute Hybrid Runbook Worker y las interacciones entre distintos componentes.</span><span class="sxs-lookup"><span data-stu-id="9db1a-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker tooexecute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="9db1a-147">toolearn acerca de cómo ejecutar runbooks de automatización en su centro de datos, consulte demasiado[hybrid runbook Worker](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="9db1a-147">toolearn about executing Automation runbooks in your datacenter, refer too[hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Arquitectura de runbook](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a><span data-ttu-id="9db1a-149">A partir de un runbook Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9db1a-149">Starting a runbook with hello Azure portal</span></span>
1. <span data-ttu-id="9db1a-150">Hola portal de Azure, seleccione **automatización** y, a continuación, haga clic en nombre de Hola de una cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="9db1a-150">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="9db1a-151">En el menú del concentrador hello, seleccione **Runbooks**.</span><span class="sxs-lookup"><span data-stu-id="9db1a-151">On hello Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="9db1a-152">En hello **Runbooks** hoja, seleccione un runbook y, a continuación, haga clic en **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="9db1a-152">On hello **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="9db1a-153">Si Hola runbook tiene parámetros, es posible que tooprovide solicitadas valores con un cuadro de texto para cada parámetro.</span><span class="sxs-lookup"><span data-stu-id="9db1a-153">If hello runbook has parameters, you will be prompted tooprovide values with a text box for each parameter.</span></span> <span data-ttu-id="9db1a-154">Consulte [Parámetros de runbook](#Runbook-parameters) a continuación para obtener más información sobre los parámetros.</span><span class="sxs-lookup"><span data-stu-id="9db1a-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="9db1a-155">En hello **trabajo** hoja, puede ver estado de Hola de trabajo de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="9db1a-155">On hello **Job** blade, you can view hello status of hello runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="9db1a-156">Inicio de un runbook con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="9db1a-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="9db1a-157">Puede usar hello [AzureRmAutomationRunbook inicio](https://msdn.microsoft.com/library/mt603661.aspx) toostart un runbook con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9db1a-157">You can use hello [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a runbook with Windows PowerShell.</span></span> <span data-ttu-id="9db1a-158">Hello código de ejemplo siguiente inicia un runbook denominado Test-Runbook.</span><span class="sxs-lookup"><span data-stu-id="9db1a-158">hello following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="9db1a-159">Inicio AzureRmAutomationRunbook devuelve un trabajo de un objeto que se puede usar tootrack su estado una vez que se inicie el runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="9db1a-159">Start-AzureRmAutomationRunbook returns a job object that you can use tootrack its status once hello runbook is started.</span></span> <span data-ttu-id="9db1a-160">A continuación, puede utilizar este objeto de trabajo con [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine estado de Hola de trabajo de Hola y [AzureRmAutomationJobOutput Get](https://msdn.microsoft.com/library/mt603476.aspx) tooget su salida.</span><span class="sxs-lookup"><span data-stu-id="9db1a-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello status of hello job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget its output.</span></span> <span data-ttu-id="9db1a-161">Hola siguiendo el ejemplo de código inicia un runbook denominado Test-Runbook, espera hasta que se ha completado y, a continuación, muestra su salida.</span><span class="sxs-lookup"><span data-stu-id="9db1a-161">hello following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

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

<span data-ttu-id="9db1a-162">Si Hola runbook requiere parámetros, debe proporcionarlos como una [hashtable](http://technet.microsoft.com/library/hh847780.aspx) donde clave Hola de tabla hash de hello coincide con el nombre del parámetro de Hola y el valor de hello es el valor del parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="9db1a-162">If hello runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key of hello hashtable matches hello parameter name and hello value is hello parameter value.</span></span> <span data-ttu-id="9db1a-163">Hello en el ejemplo siguiente se muestra cómo toostart un runbook con dos parámetros de cadena denominado FirstName y LastName, un número entero denominado RepeatCount y un parámetro booleano denominado Show.</span><span class="sxs-lookup"><span data-stu-id="9db1a-163">hello following example shows how toostart a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="9db1a-164">Para obtener información adicional sobre los parámetros, consulte [Parámetros de runbook](#Runbook-parameters) a continuación.</span><span class="sxs-lookup"><span data-stu-id="9db1a-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="9db1a-165">Parámetros de runbook</span><span class="sxs-lookup"><span data-stu-id="9db1a-165">Runbook parameters</span></span>
<span data-ttu-id="9db1a-166">Cuando se inicia un runbook desde Hola Portal de Azure o Windows PowerShell, instrucción de Hola se envía a través de hello servicio web automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="9db1a-166">When you start a runbook from hello Azure Portal or Windows PowerShell, hello instruction is sent through hello Azure Automation web service.</span></span> <span data-ttu-id="9db1a-167">Este servicio no admite parámetros con tipos de datos complejos.</span><span class="sxs-lookup"><span data-stu-id="9db1a-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="9db1a-168">Si necesita tooprovide un valor para un parámetro complejo, debe llamarlo en línea desde otro runbook como se describe en [runbooks secundarios en automatización de Azure](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="9db1a-168">If you need tooprovide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="9db1a-169">Hola servicio web automatización de Azure proporcionará funciones especiales para los parámetros mediante ciertos tipos de datos como se describe en las secciones siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="9db1a-169">hello Azure Automation web service will provide special functionality for parameters using certain data types as described in hello following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="9db1a-170">Valores con nombre</span><span class="sxs-lookup"><span data-stu-id="9db1a-170">Named values</span></span>
<span data-ttu-id="9db1a-171">Si parámetro hello es el tipo de datos [objeto], puede usar Hola después toosend de formato JSON, una lista de valores con nombre: *{nombre1: 'Value1', nombre2: 'Valor2', Nombre3: 'Value3'}*.</span><span class="sxs-lookup"><span data-stu-id="9db1a-171">If hello parameter is data type [object], then you can use hello following JSON format toosend it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="9db1a-172">Estos valores deben ser tipos simples.</span><span class="sxs-lookup"><span data-stu-id="9db1a-172">These values must be simple types.</span></span> <span data-ttu-id="9db1a-173">Hola runbook recibirá el parámetro hello como un [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) con propiedades que corresponden a tooeach con el nombre value.</span><span class="sxs-lookup"><span data-stu-id="9db1a-173">hello runbook will receive hello parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond tooeach named value.</span></span>

<span data-ttu-id="9db1a-174">Considere la posibilidad de hello siguiente runbook de prueba que acepta un parámetro denominado usuario.</span><span class="sxs-lookup"><span data-stu-id="9db1a-174">Consider hello following test runbook that accepts a parameter called user.</span></span>

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

<span data-ttu-id="9db1a-175">Hello texto siguiente podría utilizarse para el parámetro de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="9db1a-175">hello following text could be used for hello user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="9db1a-176">Esto da como resultado Hola después de salida.</span><span class="sxs-lookup"><span data-stu-id="9db1a-176">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="9db1a-177">Matrices</span><span class="sxs-lookup"><span data-stu-id="9db1a-177">Arrays</span></span>
<span data-ttu-id="9db1a-178">Si el parámetro hello es una matriz, como [matriz] o [cadena []], puede usar Hola siguientes toosend de formato JSON, una lista de valores: *[valor1, valor2, Valor3]*.</span><span class="sxs-lookup"><span data-stu-id="9db1a-178">If hello parameter is an array such as [array] or [string[]], then you can use hello following JSON format toosend it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="9db1a-179">Estos valores deben ser tipos simples.</span><span class="sxs-lookup"><span data-stu-id="9db1a-179">These values must be simple types.</span></span>

<span data-ttu-id="9db1a-180">Considere la posibilidad de hello siguiente runbook de prueba que acepta un parámetro denominado *usuario*.</span><span class="sxs-lookup"><span data-stu-id="9db1a-180">Consider hello following test runbook that accepts a parameter called *user*.</span></span>

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

<span data-ttu-id="9db1a-181">Hello texto siguiente podría utilizarse para el parámetro de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="9db1a-181">hello following text could be used for hello user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="9db1a-182">Esto da como resultado Hola después de salida.</span><span class="sxs-lookup"><span data-stu-id="9db1a-182">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="9db1a-183">Credenciales</span><span class="sxs-lookup"><span data-stu-id="9db1a-183">Credentials</span></span>
<span data-ttu-id="9db1a-184">Si el parámetro hello es el tipo de datos **PSCredential**, puede proporcionar el nombre de Hola de una automatización de Azure [activo de credencial](automation-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="9db1a-184">If hello parameter is data type **PSCredential**, then you can provide hello name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="9db1a-185">Hola runbook recuperará la credencial de hello con nombre de Hola que especifique.</span><span class="sxs-lookup"><span data-stu-id="9db1a-185">hello runbook will retrieve hello credential with hello name that you specify.</span></span>

<span data-ttu-id="9db1a-186">Considere la posibilidad de hello siguiente runbook de prueba que acepta un parámetro denominado credencial.</span><span class="sxs-lookup"><span data-stu-id="9db1a-186">Consider hello following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="9db1a-187">Hello texto siguiente podría utilizarse para el parámetro de usuario de hello suponiendo que hubiese un activo de credencial denominado *Mi credencial*.</span><span class="sxs-lookup"><span data-stu-id="9db1a-187">hello following text could be used for hello user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="9db1a-188">Si es que Hola username de credencial de hello *jsmith*, esto da como resultado Hola después de salida.</span><span class="sxs-lookup"><span data-stu-id="9db1a-188">Assuming hello username in hello credential was *jsmith*, this results in hello following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="9db1a-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9db1a-189">Next steps</span></span>
* <span data-ttu-id="9db1a-190">arquitectura de runbook de Hello en el artículo actual proporciona una descripción general de administración de recursos de runbooks en Azure y locales con hello Hybrid Runbook Worker.</span><span class="sxs-lookup"><span data-stu-id="9db1a-190">hello runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with hello Hybrid Runbook Worker.</span></span>  <span data-ttu-id="9db1a-191">toolearn acerca de cómo ejecutar runbooks de automatización en su centro de datos, consulte demasiado[Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span><span class="sxs-lookup"><span data-stu-id="9db1a-191">toolearn about executing Automation runbooks in your datacenter, refer too[Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="9db1a-192">toolearn más información acerca de hello crear toobe runbooks modulares utilizada por otros runbooks para funciones específicas o comunes, consulte demasiado[Runbooks secundarios](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="9db1a-192">toolearn more about hello creating modular runbooks toobe used by other runbooks for specific or common functions, refer too[Child Runbooks](automation-child-runbooks.md).</span></span>

