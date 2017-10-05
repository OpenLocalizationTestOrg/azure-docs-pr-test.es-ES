---
title: Iniciar un runbook en Azure Automation | Microsoft Docs
description: "Resume los distintos métodos que pueden usarse para iniciar un runbook de Azure Automation y proporciona detalles sobre cómo utilizar Azure Portal y Windows PowerShell."
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
ms.openlocfilehash: 844831b63d5263987ed05370125fbe9f01913ab9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="f1d4a-103">Inicio de un runbook en Azure Automation</span><span class="sxs-lookup"><span data-stu-id="f1d4a-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="f1d4a-104">La tabla siguiente le ayudará a determinar el método para iniciar el runbook de Azure Automation que sea más adecuado a su escenario concreto.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-104">The following table will help you determine the method to start a runbook in Azure Automation that is most suitable to your particular scenario.</span></span> <span data-ttu-id="f1d4a-105">Este artículo incluye detalles acerca de cómo iniciar un runbook con Azure Portal y Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-105">This article includes details on starting a runbook with the Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="f1d4a-106">En otra documentación a la que puede acceder desde los siguientes vínculos se proporcionan detalles sobre los otros métodos.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-106">Details on the other methods are provided in other documentation that you can access from the links below.</span></span>

| <span data-ttu-id="f1d4a-107">**MÉTODO**</span><span class="sxs-lookup"><span data-stu-id="f1d4a-107">**METHOD**</span></span> | <span data-ttu-id="f1d4a-108">**CARACTERÍSTICAS**</span><span class="sxs-lookup"><span data-stu-id="f1d4a-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="f1d4a-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f1d4a-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="f1d4a-110">Método más sencillo con la interfaz de usuario interactiva.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="f1d4a-111">Forma para proporcionar valores de parámetro simples.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-111">Form to provide simple parameter values.</span></span><br> <li><span data-ttu-id="f1d4a-112">Seguimiento sencillo del estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-112">Easily track job state.</span></span><br> <li><span data-ttu-id="f1d4a-113">Acceso autenticado con inicio de sesión de Azure.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="f1d4a-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1d4a-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="f1d4a-115">Permite llamar desde la línea de comandos con los cmdlets de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="f1d4a-116">Puede incluirse en una solución automatizada con varios pasos.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="f1d4a-117">La solicitud se autentica con el certificado o el usuario de OAuth principal/servicio principal.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="f1d4a-118">Permite proporcionar valores de parámetro simples y complejos.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="f1d4a-119">Realizar el seguimiento del estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-119">Track job state.</span></span><br> <li><span data-ttu-id="f1d4a-120">Responder a la necesidad del cliente para admitir los cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-120">Client required to support PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="f1d4a-121">API de Azure Automation</span><span class="sxs-lookup"><span data-stu-id="f1d4a-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="f1d4a-122">El método más flexible, pero también más complejo.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="f1d4a-123">Permite llamar desde cualquier código personalizado que pueda realizar solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="f1d4a-124">La solicitud se autentica con el certificado o el usuario de OAuth principal/servicio principal.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="f1d4a-125">Permite proporcionar valores de parámetro simples y complejos.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="f1d4a-126">Realizar el seguimiento del estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-126">Track job state.</span></span> |
| [<span data-ttu-id="f1d4a-127">Webhooks</span><span class="sxs-lookup"><span data-stu-id="f1d4a-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="f1d4a-128">Permite iniciar el runbook desde una única solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="f1d4a-129">Autenticado con el token de seguridad de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="f1d4a-130">Cliente no puede invalidar los valores de parámetro especificados al crear webhook.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="f1d4a-131">El runbook puede definir un único parámetro que se rellena con los detalles de la solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-131">Runbook can define single parameter that is populated with the HTTP request details.</span></span><br> <li><span data-ttu-id="f1d4a-132">No tiene capacidad de realizar un seguimiento del estado del trabajo a través de la dirección URL de webhook.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-132">No ability to track job state through webhook URL.</span></span> |
| [<span data-ttu-id="f1d4a-133">Respuesta a una alerta de Azure</span><span class="sxs-lookup"><span data-stu-id="f1d4a-133">Respond to Azure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="f1d4a-134">Permite iniciar un runbook en respuesta a una alerta de Azure.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-134">Start a runbook in response to Azure alert.</span></span><br> <li><span data-ttu-id="f1d4a-135">Permite configurar webhook para el runbook y vincular a la alerta.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-135">Configure webhook for runbook and link to alert.</span></span><br> <li><span data-ttu-id="f1d4a-136">Autenticado con el token de seguridad de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="f1d4a-137">Programación</span><span class="sxs-lookup"><span data-stu-id="f1d4a-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="f1d4a-138">Permite iniciar automáticamente el runbook en una programación según la hora, diaria, semanal o mensual.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="f1d4a-139">Permite manipular la programación a través de Azure Portal, los cmdlets de PowerShell o la API de Azure.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="f1d4a-140">Permite proporcionar valores de parámetro que se usarán con la programación.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-140">Provide parameter values to be used with schedule.</span></span> |
| [<span data-ttu-id="f1d4a-141">Desde otro Runbook</span><span class="sxs-lookup"><span data-stu-id="f1d4a-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="f1d4a-142">Permite usar un runbook como una actividad en otro runbook.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="f1d4a-143">Es útil para la funcionalidad utilizada por varios runbooks.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="f1d4a-144">Permite proporcionar valores de parámetro a un runbook secundario y usar la salida de un runbook principal.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-144">Provide parameter values to child runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="f1d4a-145">La siguiente imagen ilustra el proceso paso a paso detallado en el ciclo de vida de un runbook.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-145">The following image illustrates detailed step-by-step process in the life cycle of a runbook.</span></span> <span data-ttu-id="f1d4a-146">En ella figuran las distintas formas de iniciar un runbook en Azure Automation, los componentes requeridos para que Hybrid Runbook Worker ejecute runbooks de Azure Automation y las interacciones entre los distintos componentes.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker to execute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="f1d4a-147">Para obtener información sobre cómo ejecutar runbooks de Automation en su centro de datos, consulte [Trabajos híbridos de runbook](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="f1d4a-147">To learn about executing Automation runbooks in your datacenter, refer to [hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Arquitectura de runbook](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-the-azure-portal"></a><span data-ttu-id="f1d4a-149">Inicio de un runbook con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f1d4a-149">Starting a runbook with the Azure portal</span></span>
1. <span data-ttu-id="f1d4a-150">En Azure Portal, seleccione **Automation** y, a continuación, haga clic en el nombre de una cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-150">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="f1d4a-151">En el menú central, seleccione **Runbooks**.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-151">On the Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="f1d4a-152">En la hoja **Runbooks**, seleccione un runbook y haga clic en **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-152">On the **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="f1d4a-153">Si el runbook tiene parámetros, se le pedirá que proporcione los valores de cada parámetro con un cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-153">If the runbook has parameters, you will be prompted to provide values with a text box for each parameter.</span></span> <span data-ttu-id="f1d4a-154">Consulte [Parámetros de runbook](#Runbook-parameters) a continuación para obtener más información sobre los parámetros.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="f1d4a-155">En la hoja **Trabajo**, puede ver el estado del trabajo de runbook.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-155">On the **Job** blade, you can view the status of the runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="f1d4a-156">Inicio de un runbook con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1d4a-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="f1d4a-157">Puede utilizar [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) para iniciar un runbook con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-157">You can use the [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a runbook with Windows PowerShell.</span></span> <span data-ttu-id="f1d4a-158">El código de ejemplo siguiente inicia un runbook llamado Test-Runbook.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-158">The following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="f1d4a-159">Start-AzureRmAutomationRunbook devuelve un objeto de trabajo que puede usar para realizar un seguimiento de su estado una vez que se inicia el runbook.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-159">Start-AzureRmAutomationRunbook returns a job object that you can use to track its status once the runbook is started.</span></span> <span data-ttu-id="f1d4a-160">Después, puede utilizar este objeto de trabajo con [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) para determinar el estado del trabajo y con [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) para obtener su salida.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) to determine the status of the job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) to get its output.</span></span> <span data-ttu-id="f1d4a-161">El código de ejemplo siguiente inicia un runbook llamado Test-Runbook, espera hasta que se ha completado y después muestra la salida.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-161">The following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

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

<span data-ttu-id="f1d4a-162">Si el runbook requiere parámetros, debe proporcionarlos como una [tabla hash](http://technet.microsoft.com/library/hh847780.aspx) donde la clave de la tabla hash coincide con el nombre del parámetro y el valor es el valor del parámetro.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-162">If the runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key of the hashtable matches the parameter name and the value is the parameter value.</span></span> <span data-ttu-id="f1d4a-163">En el ejemplo siguiente se muestra cómo iniciar un runbook con dos parámetros de cadena denominados FirstName y LastName, un número entero denominado RepeatCount y un parámetro booleano denominado Show.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-163">The following example shows how to start a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="f1d4a-164">Para obtener información adicional sobre los parámetros, consulte [Parámetros de runbook](#Runbook-parameters) a continuación.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="f1d4a-165">Parámetros de runbook</span><span class="sxs-lookup"><span data-stu-id="f1d4a-165">Runbook parameters</span></span>
<span data-ttu-id="f1d4a-166">Cuando se inicia un runbook desde Azure Portal o Windows PowerShell, la instrucción se envía a través del servicio web Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-166">When you start a runbook from the Azure Portal or Windows PowerShell, the instruction is sent through the Azure Automation web service.</span></span> <span data-ttu-id="f1d4a-167">Este servicio no admite parámetros con tipos de datos complejos.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="f1d4a-168">Si necesita proporcionar un valor para un parámetro complejo, se debe llamar en línea desde otro runbook, tal como se describe en [Runbooks secundarios en Azure Automation](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="f1d4a-168">If you need to provide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="f1d4a-169">El servicio web Azure Automation proporciona una funcionalidad especial para parámetros mediante ciertos tipos de datos, tal como se describe en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-169">The Azure Automation web service will provide special functionality for parameters using certain data types as described in the following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="f1d4a-170">Valores con nombre</span><span class="sxs-lookup"><span data-stu-id="f1d4a-170">Named values</span></span>
<span data-ttu-id="f1d4a-171">Si el parámetro tiene el tipo de datos [object], puede usar el siguiente formato JSON para enviar una lista de valores con nombre: *{"Nombre1":Valor1, "Nombre2":Valor2, "Nombre3":Valor3}*.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-171">If the parameter is data type [object], then you can use the following JSON format to send it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="f1d4a-172">Estos valores deben ser tipos simples.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-172">These values must be simple types.</span></span> <span data-ttu-id="f1d4a-173">El runbook recibirá el parámetro como un [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) con propiedades que se corresponden a cada valor con nombre.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-173">The runbook will receive the parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond to each named value.</span></span>

<span data-ttu-id="f1d4a-174">Considere el siguiente runbook de prueba que acepta un parámetro denominado user.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-174">Consider the following test runbook that accepts a parameter called user.</span></span>

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

<span data-ttu-id="f1d4a-175">El texto siguiente podría utilizarse para el parámetro de usuario.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-175">The following text could be used for the user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="f1d4a-176">Esta acción devuelve la siguiente salida:</span><span class="sxs-lookup"><span data-stu-id="f1d4a-176">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="f1d4a-177">Matrices</span><span class="sxs-lookup"><span data-stu-id="f1d4a-177">Arrays</span></span>
<span data-ttu-id="f1d4a-178">Si el parámetro es una matriz como [array] o [string], puede usar entonces el siguiente formato JSON para enviarle una lista de valores: *[Value1,Value2,Value3]*.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-178">If the parameter is an array such as [array] or [string[]], then you can use the following JSON format to send it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="f1d4a-179">Estos valores deben ser tipos simples.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-179">These values must be simple types.</span></span>

<span data-ttu-id="f1d4a-180">Considere el siguiente runbook de prueba que acepta un parámetro denominado *user*.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-180">Consider the following test runbook that accepts a parameter called *user*.</span></span>

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

<span data-ttu-id="f1d4a-181">El texto siguiente podría utilizarse para el parámetro de usuario.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-181">The following text could be used for the user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="f1d4a-182">Esta acción devuelve la siguiente salida:</span><span class="sxs-lookup"><span data-stu-id="f1d4a-182">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="f1d4a-183">Credenciales</span><span class="sxs-lookup"><span data-stu-id="f1d4a-183">Credentials</span></span>
<span data-ttu-id="f1d4a-184">Si el parámetro es de tipo de datos **PSCredential**, puede proporcionar el nombre de un [recurso de credenciales](automation-credentials.md)de Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-184">If the parameter is data type **PSCredential**, then you can provide the name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="f1d4a-185">El runbook recuperará la credencial con el nombre que especifique.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-185">The runbook will retrieve the credential with the name that you specify.</span></span>

<span data-ttu-id="f1d4a-186">Considere el siguiente runbook de prueba que acepta un parámetro denominado credential.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-186">Consider the following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="f1d4a-187">Podría utilizar el siguiente texto para el parámetro de usuario suponiendo que ha habido un recurso de credenciales denominado *My Credential*.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-187">The following text could be used for the user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="f1d4a-188">Suponiendo que el nombre de usuario de la credencial era *jsmith*, esto da como resultado la salida siguiente.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-188">Assuming the username in the credential was *jsmith*, this results in the following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="f1d4a-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f1d4a-189">Next steps</span></span>
* <span data-ttu-id="f1d4a-190">La arquitectura de runbook de este artículo proporciona información general sobre la administración de recursos en Azure y entornos locales con Hybrid Runbook Worker.</span><span class="sxs-lookup"><span data-stu-id="f1d4a-190">The runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with the Hybrid Runbook Worker.</span></span>  <span data-ttu-id="f1d4a-191">Para obtener información sobre cómo ejecutar runbooks de Automation en su centro de datos, consulte [Trabajos híbridos de runbook](automation-hybrid-runbook-worker.md).</span><span class="sxs-lookup"><span data-stu-id="f1d4a-191">To learn about executing Automation runbooks in your datacenter, refer to [Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="f1d4a-192">Para aprender más sobre la creación runbooks modulares para usarse por otros runbooks para funciones específicas o comunes, consulte [Runbooks secundarios](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="f1d4a-192">To learn more about the creating modular runbooks to be used by other runbooks for specific or common functions, refer to [Child Runbooks](automation-child-runbooks.md).</span></span>

