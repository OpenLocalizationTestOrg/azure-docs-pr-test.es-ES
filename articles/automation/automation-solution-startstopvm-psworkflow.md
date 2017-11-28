---
title: "Inicio y detención de máquinas virtuales con Azure Automation: flujo de trabajo de PowerShell | Microsoft Docs"
description: "Versión gráfica del escenario de Automatización de Azure con runbooks para iniciar y detener las máquinas virtuales clásicas."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: FALSE
ms.openlocfilehash: 95a7b02b0d11bf18c398daea48d16e0ead30b543
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="91dd0-103">Escenario de Automatización de Azure: inicio y detención de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="91dd0-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="91dd0-104">Este escenario de Automatización de Azure incluye runbooks para iniciar y detener las máquinas virtuales clásicas.</span><span class="sxs-lookup"><span data-stu-id="91dd0-104">This Azure Automation scenario includes runbooks to start and stop classic virtual machines.</span></span>  <span data-ttu-id="91dd0-105">Puede usar este escenario para cualquiera de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="91dd0-105">You can use this scenario for any of the following:</span></span>  

* <span data-ttu-id="91dd0-106">Usar los runbooks sin modificaciones en su propio entorno.</span><span class="sxs-lookup"><span data-stu-id="91dd0-106">Use the runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="91dd0-107">Modificar los runbooks para ejecutar la funcionalidad personalizada.</span><span class="sxs-lookup"><span data-stu-id="91dd0-107">Modify the runbooks to perform customized functionality.</span></span>  
* <span data-ttu-id="91dd0-108">Llamar a los runbooks desde otro runbook como parte de una solución global.</span><span class="sxs-lookup"><span data-stu-id="91dd0-108">Call the runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="91dd0-109">Usar los runbooks como tutoriales para aprender los conceptos de creación de runbooks.</span><span class="sxs-lookup"><span data-stu-id="91dd0-109">Use the runbooks as tutorials to learn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="91dd0-110">Gráfico</span><span class="sxs-lookup"><span data-stu-id="91dd0-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="91dd0-111">Flujo de trabajo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="91dd0-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="91dd0-112">Es la versión de runbook del flujo de trabajo de PowerShell de este escenario.</span><span class="sxs-lookup"><span data-stu-id="91dd0-112">This is the PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="91dd0-113">Está también disponible mediante [runbooks gráficos](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="91dd0-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-the-scenario"></a><span data-ttu-id="91dd0-114">Obtención del escenario</span><span class="sxs-lookup"><span data-stu-id="91dd0-114">Getting the scenario</span></span>
<span data-ttu-id="91dd0-115">Este escenario consta de dos runbooks de flujo de trabajo de PowerShell que se pueden descargar en los vínculos siguientes.</span><span class="sxs-lookup"><span data-stu-id="91dd0-115">This scenario consists of two PowerShell Workflow runbooks that you can download from the following links.</span></span>  <span data-ttu-id="91dd0-116">Consulte la [versión gráfica](automation-solution-startstopvm-graphical.md) de este escenario para obtener vínculos a los runbooks gráficos.</span><span class="sxs-lookup"><span data-stu-id="91dd0-116">See the [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links to the graphical runbooks.</span></span>

| <span data-ttu-id="91dd0-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="91dd0-117">Runbook</span></span> | <span data-ttu-id="91dd0-118">Vínculo</span><span class="sxs-lookup"><span data-stu-id="91dd0-118">Link</span></span> | <span data-ttu-id="91dd0-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="91dd0-119">Type</span></span> | <span data-ttu-id="91dd0-120">Description</span><span class="sxs-lookup"><span data-stu-id="91dd0-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="91dd0-121">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="91dd0-121">Start-AzureVMs</span></span> |[<span data-ttu-id="91dd0-122">Inicio de máquinas virtuales de Azure clásicas</span><span class="sxs-lookup"><span data-stu-id="91dd0-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="91dd0-123">Flujo de trabajo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="91dd0-123">PowerShell Workflow</span></span> |<span data-ttu-id="91dd0-124">Inicia todas las máquinas virtuales clásicas en una suscripción de Azure o en todas las máquinas virtuales con un nombre de servicio determinado.</span><span class="sxs-lookup"><span data-stu-id="91dd0-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="91dd0-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="91dd0-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="91dd0-126">Detención de máquinas virtuales de Azure clásicas</span><span class="sxs-lookup"><span data-stu-id="91dd0-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="91dd0-127">Flujo de trabajo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="91dd0-127">PowerShell Workflow</span></span> |<span data-ttu-id="91dd0-128">Detiene todas las máquinas virtuales de una cuenta de automatización o todas las máquinas virtuales con un nombre de servicio determinado.</span><span class="sxs-lookup"><span data-stu-id="91dd0-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-the-scenario"></a><span data-ttu-id="91dd0-129">Instalación y configuración del escenario</span><span class="sxs-lookup"><span data-stu-id="91dd0-129">Installing and configuring the scenario</span></span>
### <a name="1-install-the-runbooks"></a><span data-ttu-id="91dd0-130">1. Instalación de los runbooks</span><span class="sxs-lookup"><span data-stu-id="91dd0-130">1. Install the runbooks</span></span>
<span data-ttu-id="91dd0-131">Después de descargar los runbooks, puede importarlos mediante el procedimiento descrito en [Importación de un runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span><span class="sxs-lookup"><span data-stu-id="91dd0-131">After downloading the runbooks, you can import them using the procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-the-description-and-requirements"></a><span data-ttu-id="91dd0-132">2. Revisión de la descripción y los requisitos</span><span class="sxs-lookup"><span data-stu-id="91dd0-132">2. Review the description and requirements</span></span>
<span data-ttu-id="91dd0-133">Los runbooks incluyen el texto de ayuda comentada que incluye una descripción y los activos necesarios.</span><span class="sxs-lookup"><span data-stu-id="91dd0-133">The runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="91dd0-134">También puede obtener la misma información en este artículo.</span><span class="sxs-lookup"><span data-stu-id="91dd0-134">You can also get the same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="91dd0-135">3. Configuración de activos</span><span class="sxs-lookup"><span data-stu-id="91dd0-135">3. Configure assets</span></span>
<span data-ttu-id="91dd0-136">Los runbooks requieren los siguientes activos que se deben crear y rellenar con los valores adecuados.</span><span class="sxs-lookup"><span data-stu-id="91dd0-136">The runbooks require the following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="91dd0-137">Tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="91dd0-137">Asset Type</span></span> | <span data-ttu-id="91dd0-138">Nombre de recurso</span><span class="sxs-lookup"><span data-stu-id="91dd0-138">Asset Name</span></span> | <span data-ttu-id="91dd0-139">Description</span><span class="sxs-lookup"><span data-stu-id="91dd0-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="91dd0-140">Credential:</span><span class="sxs-lookup"><span data-stu-id="91dd0-140">Credential</span></span> |<span data-ttu-id="91dd0-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="91dd0-141">AzureCredential</span></span> |<span data-ttu-id="91dd0-142">Contiene las credenciales para una cuenta que tiene autoridad para iniciar y detener las máquinas virtuales en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="91dd0-142">Contains credentials for an account that has authority to start and stop virtual machines in the Azure subscription.</span></span>  <span data-ttu-id="91dd0-143">Además, puede especificar otro recurso de credenciales en el parámetro **Credential** de la actividad **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="91dd0-143">Alternatively, you can specify another credential asset in the **Credential** parameter of the **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="91dd0-144">Variable</span><span class="sxs-lookup"><span data-stu-id="91dd0-144">Variable</span></span> |<span data-ttu-id="91dd0-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="91dd0-145">AzureSubscriptionId</span></span> |<span data-ttu-id="91dd0-146">Contiene el identificador de suscripción de su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="91dd0-146">Contains the subscription ID of your Azure subscription.</span></span> |

## <a name="using-the-scenario"></a><span data-ttu-id="91dd0-147">Uso del escenario</span><span class="sxs-lookup"><span data-stu-id="91dd0-147">Using the scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="91dd0-148">Parámetros</span><span class="sxs-lookup"><span data-stu-id="91dd0-148">Parameters</span></span>
<span data-ttu-id="91dd0-149">Los runbooks tienen los siguientes parámetros.</span><span class="sxs-lookup"><span data-stu-id="91dd0-149">The runbooks each have the following parameters.</span></span>  <span data-ttu-id="91dd0-150">Debe proporcionar valores para los parámetros obligatorios y opcionalmente puede proporcionar valores para otros parámetros dependiendo de sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="91dd0-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="91dd0-151">Parámetro</span><span class="sxs-lookup"><span data-stu-id="91dd0-151">Parameter</span></span> | <span data-ttu-id="91dd0-152">Escriba</span><span class="sxs-lookup"><span data-stu-id="91dd0-152">Type</span></span> | <span data-ttu-id="91dd0-153">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="91dd0-153">Mandatory</span></span> | <span data-ttu-id="91dd0-154">Descripción</span><span class="sxs-lookup"><span data-stu-id="91dd0-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="91dd0-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="91dd0-155">ServiceName</span></span> |<span data-ttu-id="91dd0-156">cadena</span><span class="sxs-lookup"><span data-stu-id="91dd0-156">string</span></span> |<span data-ttu-id="91dd0-157">No</span><span class="sxs-lookup"><span data-stu-id="91dd0-157">No</span></span> |<span data-ttu-id="91dd0-158">Si se proporciona un valor, todas las máquinas virtuales con ese nombre de servicio se inician o se detienen.</span><span class="sxs-lookup"><span data-stu-id="91dd0-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="91dd0-159">Si no se proporciona un valor, todas las máquinas virtuales clásicas de la suscripción de Azure se inician o se detienen.</span><span class="sxs-lookup"><span data-stu-id="91dd0-159">If no value is provided, then all classic virtual machines in the Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="91dd0-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="91dd0-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="91dd0-161">cadena</span><span class="sxs-lookup"><span data-stu-id="91dd0-161">string</span></span> |<span data-ttu-id="91dd0-162">No</span><span class="sxs-lookup"><span data-stu-id="91dd0-162">No</span></span> |<span data-ttu-id="91dd0-163">Contiene el nombre del [recurso de variables](#installing-and-configuring-the-scenario) que contiene a su vez el identificador de suscripción de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="91dd0-163">Contains the name of the [variable asset](#installing-and-configuring-the-scenario) that contains the subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="91dd0-164">Si no se especifica un valor, se usa *AzureSubscriptionId* .</span><span class="sxs-lookup"><span data-stu-id="91dd0-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="91dd0-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="91dd0-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="91dd0-166">cadena</span><span class="sxs-lookup"><span data-stu-id="91dd0-166">string</span></span> |<span data-ttu-id="91dd0-167">No</span><span class="sxs-lookup"><span data-stu-id="91dd0-167">No</span></span> |<span data-ttu-id="91dd0-168">Contiene el nombre del [activo de credenciales](#installing-and-configuring-the-scenario) que contiene las credenciales que usará el runbook.</span><span class="sxs-lookup"><span data-stu-id="91dd0-168">Contains the name of the [credential asset](#installing-and-configuring-the-scenario) that contains the credentials for the runbook to use.</span></span>  <span data-ttu-id="91dd0-169">Si no se especifica un valor, se usa *AzureCredential* .</span><span class="sxs-lookup"><span data-stu-id="91dd0-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-the-runbooks"></a><span data-ttu-id="91dd0-170">Inicio de los runbooks</span><span class="sxs-lookup"><span data-stu-id="91dd0-170">Starting the runbooks</span></span>
<span data-ttu-id="91dd0-171">Puede usar cualquiera de los métodos de [Inicio de un runbook en Automatización de Azure](automation-starting-a-runbook.md) para iniciar los runbooks de este escenario.</span><span class="sxs-lookup"><span data-stu-id="91dd0-171">You can use any of the methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to start either of the runbooks in this scenario.</span></span>

<span data-ttu-id="91dd0-172">Los siguientes comandos de ejemplo usan Windows PowerShell para ejecutar **StartAzureVMs** para iniciar todas las máquinas virtuales con el nombre del servicio *MyVMService*.</span><span class="sxs-lookup"><span data-stu-id="91dd0-172">The following sample commands uses Windows PowerShell to run **StartAzureVMs** to start all virtual machines with the service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="91dd0-173">Salida</span><span class="sxs-lookup"><span data-stu-id="91dd0-173">Output</span></span>
<span data-ttu-id="91dd0-174">Los runbooks [enviarán un mensaje](automation-runbook-output-and-messages.md) para cada máquina virtual indicando si se ha enviado correctamente la instrucción para iniciar o detener.</span><span class="sxs-lookup"><span data-stu-id="91dd0-174">The runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not the start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="91dd0-175">Puede buscar una cadena concreta en la salida para determinar el resultado para cada runbook.</span><span class="sxs-lookup"><span data-stu-id="91dd0-175">You can look for a specific string in the output to determine the result for each runbook.</span></span>  <span data-ttu-id="91dd0-176">En la tabla siguiente se muestran las posibles cadenas de salida.</span><span class="sxs-lookup"><span data-stu-id="91dd0-176">The possible output strings are listed in the following table.</span></span>

| <span data-ttu-id="91dd0-177">Runbook</span><span class="sxs-lookup"><span data-stu-id="91dd0-177">Runbook</span></span> | <span data-ttu-id="91dd0-178">Condición</span><span class="sxs-lookup"><span data-stu-id="91dd0-178">Condition</span></span> | <span data-ttu-id="91dd0-179">Message</span><span class="sxs-lookup"><span data-stu-id="91dd0-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="91dd0-180">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="91dd0-180">Start-AzureVMs</span></span> |<span data-ttu-id="91dd0-181">La máquina virtual ya se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="91dd0-181">Virtual machine is already running</span></span> |<span data-ttu-id="91dd0-182">MyVM ya se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="91dd0-182">MyVM is already running</span></span> |
| <span data-ttu-id="91dd0-183">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="91dd0-183">Start-AzureVMs</span></span> |<span data-ttu-id="91dd0-184">La solicitud de inicio de la máquina virtual ha enviado correctamente.</span><span class="sxs-lookup"><span data-stu-id="91dd0-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="91dd0-185">Se ha iniciado MyVM.</span><span class="sxs-lookup"><span data-stu-id="91dd0-185">MyVM has been started</span></span> |
| <span data-ttu-id="91dd0-186">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="91dd0-186">Start-AzureVMs</span></span> |<span data-ttu-id="91dd0-187">Se produjo un error en la solicitud de inicio de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="91dd0-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="91dd0-188">La MyVM no se pudo iniciar.</span><span class="sxs-lookup"><span data-stu-id="91dd0-188">MyVM failed to start</span></span> |
| <span data-ttu-id="91dd0-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="91dd0-189">Stop-AzureVMs</span></span> |<span data-ttu-id="91dd0-190">La máquina virtual ya se ha detenido</span><span class="sxs-lookup"><span data-stu-id="91dd0-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="91dd0-191">MyVM ya se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="91dd0-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="91dd0-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="91dd0-192">Stop-AzureVMs</span></span> |<span data-ttu-id="91dd0-193">La solicitud de detención de la máquina virtual ha enviado correctamente</span><span class="sxs-lookup"><span data-stu-id="91dd0-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="91dd0-194">Se ha detenido MyVM</span><span class="sxs-lookup"><span data-stu-id="91dd0-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="91dd0-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="91dd0-195">Stop-AzureVMs</span></span> |<span data-ttu-id="91dd0-196">Se produjo un error en la solicitud de detención de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="91dd0-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="91dd0-197">La MyVM no se pudo detener</span><span class="sxs-lookup"><span data-stu-id="91dd0-197">MyVM failed to stop</span></span> |

<span data-ttu-id="91dd0-198">Por ejemplo, el siguiente fragmento de código de un runbook intenta iniciar todas las máquinas virtuales con el nombre de servicio *MyServiceName*.</span><span class="sxs-lookup"><span data-stu-id="91dd0-198">For example, the following code snippet from a runbook attempts to start all virtual machines with the service name *MyServiceName*.</span></span>  <span data-ttu-id="91dd0-199">Si se produce un error en las solicitudes de inicio, se pueden realizar acciones de error.</span><span class="sxs-lookup"><span data-stu-id="91dd0-199">If any of the start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action to take in case of success.
        }
        else {
            # Action to take in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="91dd0-200">Desglose detallado</span><span class="sxs-lookup"><span data-stu-id="91dd0-200">Detailed breakdown</span></span>
<span data-ttu-id="91dd0-201">Lo siguiente es un desglose detallado de los runbooks de este escenario.</span><span class="sxs-lookup"><span data-stu-id="91dd0-201">Following is a detailed breakdown of the runbooks in this scenario.</span></span>  <span data-ttu-id="91dd0-202">Puede usar esta información para personalizar los runbooks o solo para aprender de ellos para crear sus propios escenarios de automatización.</span><span class="sxs-lookup"><span data-stu-id="91dd0-202">You can use this information to either customize the runbooks or just to learn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="91dd0-203">Parámetros</span><span class="sxs-lookup"><span data-stu-id="91dd0-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="91dd0-204">El flujo de trabajo se inicia al obtener los valores de los [parámetros de entrada](#using-the-scenario).</span><span class="sxs-lookup"><span data-stu-id="91dd0-204">The workflow starts by getting the values for the [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="91dd0-205">Si no se proporcionan los nombres de activos, se usan nombres predeterminados.</span><span class="sxs-lookup"><span data-stu-id="91dd0-205">If the asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="91dd0-206">Salida</span><span class="sxs-lookup"><span data-stu-id="91dd0-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="91dd0-207">Esta línea declara que la salida del runbook será una cadena.</span><span class="sxs-lookup"><span data-stu-id="91dd0-207">This line declares that the output of the runbook will be a string.</span></span>  <span data-ttu-id="91dd0-208">Esto no es necesario, pero es una práctica recomendada para cuando el runbook se usa como un [runbook secundario](automation-child-runbooks.md) para que sepa el tipo de salida puede esperar un runbook primario.</span><span class="sxs-lookup"><span data-stu-id="91dd0-208">This is not required but is a best practice for when the runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know the output type to expect.</span></span>

### <a name="authentication"></a><span data-ttu-id="91dd0-209">Autenticación</span><span class="sxs-lookup"><span data-stu-id="91dd0-209">Authentication</span></span>
    # Connect to Azure and select the subscription to work against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="91dd0-210">Las líneas siguientes establecen las [credenciales](automation-credentials.md) y la suscripción de Azure que se usarán para el resto del runbook.</span><span class="sxs-lookup"><span data-stu-id="91dd0-210">The next lines set the [credentials](automation-credentials.md) and Azure subscription that will be used for the rest of the runbook.</span></span>
<span data-ttu-id="91dd0-211">Primero se usa **Get-AutomationPSCredential** para obtener el activo que contiene las credenciales con acceso para iniciar y detener las máquinas virtuales en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="91dd0-211">First we use **Get-AutomationPSCredential** to get the asset that holds the credentials with access to start and stop virtual machines in the Azure subscription.</span></span> <span data-ttu-id="91dd0-212">**Add-AzureAccount** usa después este activo para establecer las credenciales.</span><span class="sxs-lookup"><span data-stu-id="91dd0-212">**Add-AzureAccount** then uses this asset to set the credentials.</span></span>  <span data-ttu-id="91dd0-213">La salida se asigna a una variable ficticia para que no se incluya en la salida del runbook.</span><span class="sxs-lookup"><span data-stu-id="91dd0-213">The output is assigned to a dummy variable so that it isn't included in the runbook output.</span></span>  

<span data-ttu-id="91dd0-214">El recurso de variables con el identificador de suscripción se recupera con **Get-AutomationVariable** y la suscripción establecida con **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="91dd0-214">The variable asset with the subscription ID is then retrieved with **Get-AutomationVariable** and the subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="91dd0-215">Get VMs</span><span class="sxs-lookup"><span data-stu-id="91dd0-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in the service,
    # otherwise get all VMs in the subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="91dd0-216">**Get-AzureVM** se usa para recuperar las máquinas virtuales con las que funciona el runbook.</span><span class="sxs-lookup"><span data-stu-id="91dd0-216">**Get-AzureVM** is used to retrieve the virtual machines the runbook will work with.</span></span>  <span data-ttu-id="91dd0-217">Si se proporciona un valor en la variable de entrada **ServiceName** , se recuperan solo las máquinas virtuales con ese nombre de servicio.</span><span class="sxs-lookup"><span data-stu-id="91dd0-217">If a value is provided in the **ServiceName** input variable, then only the virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="91dd0-218">Si **ServiceName** está vacío, se recuperan todas las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="91dd0-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="91dd0-219">Inicio o detención de máquinas virtuales y envío de resultados</span><span class="sxs-lookup"><span data-stu-id="91dd0-219">Start/Stop virtual machines and send output</span></span>
    # Start each of the stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # The VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # The VM needs to be started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # The VM failed to start, so send notice
                Write-Output ($VM.InstanceName + " failed to start")
            }
            else
            {
                # The VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="91dd0-220">Las líneas siguientes recorren cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="91dd0-220">The next lines step through each virtual machine.</span></span>  <span data-ttu-id="91dd0-221">Primero se comprueba el **PowerState** de la máquina virtual para ver si se ejecuta o se detiene, dependiendo del runbook.</span><span class="sxs-lookup"><span data-stu-id="91dd0-221">First the **PowerState** of the virtual machine is checked to see if it is already running or stopped, depending on the runbook.</span></span>  <span data-ttu-id="91dd0-222">Si ya está en el estado de destino, se envía un mensaje a la salida y el runbook finaliza.</span><span class="sxs-lookup"><span data-stu-id="91dd0-222">If it is already in the target state, then a message is sent to output, and the runbook ends.</span></span>  <span data-ttu-id="91dd0-223">Si no lo está, se usa **Start-AzureVM** o **Stop-AzureVM** para intentar iniciar o detener la máquina virtual con el resultado de la solicitud que se almacena en una variable.</span><span class="sxs-lookup"><span data-stu-id="91dd0-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used to attempt to start or stop the virtual machine with the result of the request stored to a variable.</span></span>  <span data-ttu-id="91dd0-224">Después se envía un mensaje a la salida con la especificación de si se envió correctamente la solicitud para iniciar o detener.</span><span class="sxs-lookup"><span data-stu-id="91dd0-224">A message is then sent to output specifying whether the request to start or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91dd0-225">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="91dd0-225">Next steps</span></span>
* <span data-ttu-id="91dd0-226">Para obtener más información sobre cómo trabajar con Runbooks secundarios, vea [Runbooks secundarios en la Automatización de Azure](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="91dd0-226">To learn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="91dd0-227">Para obtener más información sobre los mensajes de salida durante la ejecución de un Runbook y el inicio de sesión para ayudar en la solución de problemas, vea [Salidas de Runbook y mensajes en la Automatización de Azure](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="91dd0-227">To learn more about output messages during runbook execution and logging to help troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

