---
title: "aaaStarting y la detención máquinas virtuales con automatización de Azure: flujo de trabajo de PowerShell | Documentos de Microsoft"
description: "Versión gráfica del escenario de automatización de Azure incluidos runbooks toostart y detener máquinas virtuales clásicas."
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
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="ae7a0-103">Escenario de Automatización de Azure: inicio y detención de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="ae7a0-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="ae7a0-104">Este escenario de automatización de Azure incluye runbooks toostart y detener máquinas virtuales clásicas.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-104">This Azure Automation scenario includes runbooks toostart and stop classic virtual machines.</span></span>  <span data-ttu-id="ae7a0-105">Puede usar este escenario para cualquiera de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="ae7a0-105">You can use this scenario for any of hello following:</span></span>  

* <span data-ttu-id="ae7a0-106">Usar runbooks de hello sin modificaciones en su propio entorno.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-106">Use hello runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="ae7a0-107">Modificar la funcionalidad de tooperform personalizado de hello runbooks.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-107">Modify hello runbooks tooperform customized functionality.</span></span>  
* <span data-ttu-id="ae7a0-108">Llame a runbooks Hola desde otro runbook como parte de una solución global.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-108">Call hello runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="ae7a0-109">Utilizar runbooks hello como tutoriales toolearn runbook conceptos de creación.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-109">Use hello runbooks as tutorials toolearn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae7a0-110">Gráfico</span><span class="sxs-lookup"><span data-stu-id="ae7a0-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="ae7a0-111">Flujo de trabajo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae7a0-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="ae7a0-112">Se trata de hello versión de runbook de flujo de trabajo de PowerShell de este escenario.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-112">This is hello PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="ae7a0-113">Está también disponible mediante [runbooks gráficos](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="ae7a0-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-hello-scenario"></a><span data-ttu-id="ae7a0-114">Introducción al escenario de Hola</span><span class="sxs-lookup"><span data-stu-id="ae7a0-114">Getting hello scenario</span></span>
<span data-ttu-id="ae7a0-115">Este escenario consta de dos runbooks de flujo de trabajo de PowerShell que puede descargar desde Hola siguientes vínculos.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-115">This scenario consists of two PowerShell Workflow runbooks that you can download from hello following links.</span></span>  <span data-ttu-id="ae7a0-116">Vea hello [versión gráfica](automation-solution-startstopvm-graphical.md) de este escenario para runbooks gráficos toohello de vínculos.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-116">See hello [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links toohello graphical runbooks.</span></span>

| <span data-ttu-id="ae7a0-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="ae7a0-117">Runbook</span></span> | <span data-ttu-id="ae7a0-118">Vínculo</span><span class="sxs-lookup"><span data-stu-id="ae7a0-118">Link</span></span> | <span data-ttu-id="ae7a0-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="ae7a0-119">Type</span></span> | <span data-ttu-id="ae7a0-120">Description</span><span class="sxs-lookup"><span data-stu-id="ae7a0-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ae7a0-121">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="ae7a0-121">Start-AzureVMs</span></span> |[<span data-ttu-id="ae7a0-122">Inicio de máquinas virtuales de Azure clásicas</span><span class="sxs-lookup"><span data-stu-id="ae7a0-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="ae7a0-123">Flujo de trabajo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae7a0-123">PowerShell Workflow</span></span> |<span data-ttu-id="ae7a0-124">Inicia todas las máquinas virtuales clásicas en una suscripción de Azure o en todas las máquinas virtuales con un nombre de servicio determinado.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="ae7a0-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="ae7a0-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="ae7a0-126">Detención de máquinas virtuales de Azure clásicas</span><span class="sxs-lookup"><span data-stu-id="ae7a0-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="ae7a0-127">Flujo de trabajo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae7a0-127">PowerShell Workflow</span></span> |<span data-ttu-id="ae7a0-128">Detiene todas las máquinas virtuales de una cuenta de automatización o todas las máquinas virtuales con un nombre de servicio determinado.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-hello-scenario"></a><span data-ttu-id="ae7a0-129">Instalar y configurar el escenario de Hola</span><span class="sxs-lookup"><span data-stu-id="ae7a0-129">Installing and configuring hello scenario</span></span>
### <a name="1-install-hello-runbooks"></a><span data-ttu-id="ae7a0-130">1. Instalar runbooks Hola</span><span class="sxs-lookup"><span data-stu-id="ae7a0-130">1. Install hello runbooks</span></span>
<span data-ttu-id="ae7a0-131">Después de descargar runbooks hello, puede importarlos mediante el procedimiento de hello en [importar un Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span><span class="sxs-lookup"><span data-stu-id="ae7a0-131">After downloading hello runbooks, you can import them using hello procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-hello-description-and-requirements"></a><span data-ttu-id="ae7a0-132">2. Descripción de Hola de revisión y los requisitos</span><span class="sxs-lookup"><span data-stu-id="ae7a0-132">2. Review hello description and requirements</span></span>
<span data-ttu-id="ae7a0-133">Hola runbooks incluye el texto de ayuda comentados que incluye una descripción y los recursos necesarios.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-133">hello runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="ae7a0-134">También puede obtener Hola la misma información de este artículo.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-134">You can also get hello same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="ae7a0-135">3. Configuración de activos</span><span class="sxs-lookup"><span data-stu-id="ae7a0-135">3. Configure assets</span></span>
<span data-ttu-id="ae7a0-136">Hola runbooks requieren Hola después de activos que se deben crear y rellenar con los valores adecuados.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-136">hello runbooks require hello following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="ae7a0-137">Tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="ae7a0-137">Asset Type</span></span> | <span data-ttu-id="ae7a0-138">Nombre de recurso</span><span class="sxs-lookup"><span data-stu-id="ae7a0-138">Asset Name</span></span> | <span data-ttu-id="ae7a0-139">Description</span><span class="sxs-lookup"><span data-stu-id="ae7a0-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ae7a0-140">Credential:</span><span class="sxs-lookup"><span data-stu-id="ae7a0-140">Credential</span></span> |<span data-ttu-id="ae7a0-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="ae7a0-141">AzureCredential</span></span> |<span data-ttu-id="ae7a0-142">Contiene las credenciales para una cuenta que tenga autoridad toostart y detener las máquinas virtuales en hello suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-142">Contains credentials for an account that has authority toostart and stop virtual machines in hello Azure subscription.</span></span>  <span data-ttu-id="ae7a0-143">Como alternativa, puede especificar otro recurso de credencial en hello **credencial** parámetro de hello **Add-AzureAccount** actividad.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-143">Alternatively, you can specify another credential asset in hello **Credential** parameter of hello **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="ae7a0-144">Variable</span><span class="sxs-lookup"><span data-stu-id="ae7a0-144">Variable</span></span> |<span data-ttu-id="ae7a0-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="ae7a0-145">AzureSubscriptionId</span></span> |<span data-ttu-id="ae7a0-146">Contiene el Id. de suscripción de Hola de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-146">Contains hello subscription ID of your Azure subscription.</span></span> |

## <a name="using-hello-scenario"></a><span data-ttu-id="ae7a0-147">Uso de escenario de Hola</span><span class="sxs-lookup"><span data-stu-id="ae7a0-147">Using hello scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="ae7a0-148">parameters</span><span class="sxs-lookup"><span data-stu-id="ae7a0-148">Parameters</span></span>
<span data-ttu-id="ae7a0-149">Hola runbooks tienen Hola parámetros siguientes.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-149">hello runbooks each have hello following parameters.</span></span>  <span data-ttu-id="ae7a0-150">Tiene que proporcionar valores para los parámetros obligatorios y opcionalmente puede proporcionar valores para otros parámetros dependiendo de sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="ae7a0-151">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ae7a0-151">Parameter</span></span> | <span data-ttu-id="ae7a0-152">Escriba</span><span class="sxs-lookup"><span data-stu-id="ae7a0-152">Type</span></span> | <span data-ttu-id="ae7a0-153">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ae7a0-153">Mandatory</span></span> | <span data-ttu-id="ae7a0-154">Descripción</span><span class="sxs-lookup"><span data-stu-id="ae7a0-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ae7a0-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="ae7a0-155">ServiceName</span></span> |<span data-ttu-id="ae7a0-156">cadena</span><span class="sxs-lookup"><span data-stu-id="ae7a0-156">string</span></span> |<span data-ttu-id="ae7a0-157">No</span><span class="sxs-lookup"><span data-stu-id="ae7a0-157">No</span></span> |<span data-ttu-id="ae7a0-158">Si se proporciona un valor, todas las máquinas virtuales con ese nombre de servicio se inician o se detienen.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="ae7a0-159">Si no se proporciona ningún valor, todas las máquinas virtuales clásicas Hola suscripción de Azure está iniciadas o detenidas.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-159">If no value is provided, then all classic virtual machines in hello Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="ae7a0-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="ae7a0-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="ae7a0-161">cadena</span><span class="sxs-lookup"><span data-stu-id="ae7a0-161">string</span></span> |<span data-ttu-id="ae7a0-162">No</span><span class="sxs-lookup"><span data-stu-id="ae7a0-162">No</span></span> |<span data-ttu-id="ae7a0-163">Contiene el nombre hello de hello [activo de variable](#installing-and-configuring-the-scenario) que contiene el identificador de la suscripción de Hola de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-163">Contains hello name of hello [variable asset](#installing-and-configuring-the-scenario) that contains hello subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="ae7a0-164">Si no se especifica un valor, se usa *AzureSubscriptionId* .</span><span class="sxs-lookup"><span data-stu-id="ae7a0-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="ae7a0-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="ae7a0-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="ae7a0-166">cadena</span><span class="sxs-lookup"><span data-stu-id="ae7a0-166">string</span></span> |<span data-ttu-id="ae7a0-167">No</span><span class="sxs-lookup"><span data-stu-id="ae7a0-167">No</span></span> |<span data-ttu-id="ae7a0-168">Contiene el nombre hello de hello [activo de credencial](#installing-and-configuring-the-scenario) que contiene las credenciales de Hola para hello runbook toouse.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-168">Contains hello name of hello [credential asset](#installing-and-configuring-the-scenario) that contains hello credentials for hello runbook toouse.</span></span>  <span data-ttu-id="ae7a0-169">Si no se especifica un valor, se usa *AzureCredential* .</span><span class="sxs-lookup"><span data-stu-id="ae7a0-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-hello-runbooks"></a><span data-ttu-id="ae7a0-170">A partir de hello runbooks</span><span class="sxs-lookup"><span data-stu-id="ae7a0-170">Starting hello runbooks</span></span>
<span data-ttu-id="ae7a0-171">Puede usar cualquiera de los métodos de hello en [a partir de un runbook en automatización de Azure](automation-starting-a-runbook.md) toostart cualquiera de hello runbooks en este escenario.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-171">You can use any of hello methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toostart either of hello runbooks in this scenario.</span></span>

<span data-ttu-id="ae7a0-172">Siga los comandos del ejemplo de Hola usa Windows PowerShell toorun **StartAzureVMs** toostart todas las máquinas virtuales con el nombre del servicio de hello *MyVMService*.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-172">hello following sample commands uses Windows PowerShell toorun **StartAzureVMs** toostart all virtual machines with hello service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="ae7a0-173">Salida</span><span class="sxs-lookup"><span data-stu-id="ae7a0-173">Output</span></span>
<span data-ttu-id="ae7a0-174">Hola runbooks le [un mensaje de salida](automation-runbook-output-and-messages.md) para cada máquina virtual que indica Hola o no inicio o la instrucción stop se envió correctamente.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-174">hello runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not hello start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="ae7a0-175">También puede buscar una cadena concreta en hello toodetermine Hola resultado para cada runbook.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-175">You can look for a specific string in hello output toodetermine hello result for each runbook.</span></span>  <span data-ttu-id="ae7a0-176">se muestran cadenas de resultado posible de Hola en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-176">hello possible output strings are listed in hello following table.</span></span>

| <span data-ttu-id="ae7a0-177">Runbook</span><span class="sxs-lookup"><span data-stu-id="ae7a0-177">Runbook</span></span> | <span data-ttu-id="ae7a0-178">Condición</span><span class="sxs-lookup"><span data-stu-id="ae7a0-178">Condition</span></span> | <span data-ttu-id="ae7a0-179">Message</span><span class="sxs-lookup"><span data-stu-id="ae7a0-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ae7a0-180">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="ae7a0-180">Start-AzureVMs</span></span> |<span data-ttu-id="ae7a0-181">La máquina virtual ya se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-181">Virtual machine is already running</span></span> |<span data-ttu-id="ae7a0-182">MyVM ya se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-182">MyVM is already running</span></span> |
| <span data-ttu-id="ae7a0-183">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="ae7a0-183">Start-AzureVMs</span></span> |<span data-ttu-id="ae7a0-184">La solicitud de inicio de la máquina virtual ha enviado correctamente.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="ae7a0-185">Se ha iniciado MyVM.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-185">MyVM has been started</span></span> |
| <span data-ttu-id="ae7a0-186">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="ae7a0-186">Start-AzureVMs</span></span> |<span data-ttu-id="ae7a0-187">Se produjo un error en la solicitud de inicio de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ae7a0-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="ae7a0-188">MyVM no pudo toostart</span><span class="sxs-lookup"><span data-stu-id="ae7a0-188">MyVM failed toostart</span></span> |
| <span data-ttu-id="ae7a0-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="ae7a0-189">Stop-AzureVMs</span></span> |<span data-ttu-id="ae7a0-190">La máquina virtual ya se ha detenido</span><span class="sxs-lookup"><span data-stu-id="ae7a0-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="ae7a0-191">MyVM ya se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="ae7a0-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="ae7a0-192">Stop-AzureVMs</span></span> |<span data-ttu-id="ae7a0-193">La solicitud de detención de la máquina virtual ha enviado correctamente</span><span class="sxs-lookup"><span data-stu-id="ae7a0-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="ae7a0-194">Se ha detenido MyVM</span><span class="sxs-lookup"><span data-stu-id="ae7a0-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="ae7a0-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="ae7a0-195">Stop-AzureVMs</span></span> |<span data-ttu-id="ae7a0-196">Se produjo un error en la solicitud de detención de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ae7a0-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="ae7a0-197">MyVM no pudo toostop</span><span class="sxs-lookup"><span data-stu-id="ae7a0-197">MyVM failed toostop</span></span> |

<span data-ttu-id="ae7a0-198">Por ejemplo, hello siguiente fragmento de código desde un runbook intentará toostart todas las máquinas virtuales con el nombre del servicio de hello *MyServiceName*.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-198">For example, hello following code snippet from a runbook attempts toostart all virtual machines with hello service name *MyServiceName*.</span></span>  <span data-ttu-id="ae7a0-199">Si cualquiera de Hola inicia por error de las solicitudes, se pueden realizar acciones de error.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-199">If any of hello start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="ae7a0-200">Desglose detallado</span><span class="sxs-lookup"><span data-stu-id="ae7a0-200">Detailed breakdown</span></span>
<span data-ttu-id="ae7a0-201">Aquí te mostramos un análisis detallado de hello runbooks en este escenario.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-201">Following is a detailed breakdown of hello runbooks in this scenario.</span></span>  <span data-ttu-id="ae7a0-202">Puede utilizar esta información tooeither personalizar Hola runbooks o simplemente toolearn de ellos para la creación de sus propios escenarios de automatización.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-202">You can use this information tooeither customize hello runbooks or just toolearn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="ae7a0-203">parameters</span><span class="sxs-lookup"><span data-stu-id="ae7a0-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="ae7a0-204">Hello flujo de trabajo se inicia mediante la obtención de valores de hello para hello [parámetros de entrada](#using-the-scenario).</span><span class="sxs-lookup"><span data-stu-id="ae7a0-204">hello workflow starts by getting hello values for hello [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="ae7a0-205">Si no se proporcionan nombres de activos de Hola se utilizan nombres predeterminados.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-205">If hello asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="ae7a0-206">Salida</span><span class="sxs-lookup"><span data-stu-id="ae7a0-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="ae7a0-207">Esta línea declara que la salida de hello de hello runbook será una cadena.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-207">This line declares that hello output of hello runbook will be a string.</span></span>  <span data-ttu-id="ae7a0-208">Esto no es necesario, pero es una práctica recomendada para cuando se utiliza Hola runbook como un [runbook secundario](automation-child-runbooks.md) para que un runbook primario sepan salida de hello escriba tooexpect.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-208">This is not required but is a best practice for when hello runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know hello output type tooexpect.</span></span>

### <a name="authentication"></a><span data-ttu-id="ae7a0-209">Autenticación</span><span class="sxs-lookup"><span data-stu-id="ae7a0-209">Authentication</span></span>
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="ae7a0-210">en las líneas siguientes Hola establecer hello [credenciales](automation-credentials.md) y suscripción de Azure que se usará para el resto de Hola de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-210">hello next lines set hello [credentials](automation-credentials.md) and Azure subscription that will be used for hello rest of hello runbook.</span></span>
<span data-ttu-id="ae7a0-211">En primer lugar se utilice **Get-AutomationPSCredential** tooget activos de Hola que contiene las credenciales de hello con acceso toostart y deje de máquinas virtuales en hello suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-211">First we use **Get-AutomationPSCredential** tooget hello asset that holds hello credentials with access toostart and stop virtual machines in hello Azure subscription.</span></span> <span data-ttu-id="ae7a0-212">**Agregar-AzureAccount** , a continuación, usa este credenciales de hello tooset activo.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-212">**Add-AzureAccount** then uses this asset tooset hello credentials.</span></span>  <span data-ttu-id="ae7a0-213">salida de Hello se asigna la variable ficticia tooa para que no se incluye en la salida de hello runbook.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-213">hello output is assigned tooa dummy variable so that it isn't included in hello runbook output.</span></span>  

<span data-ttu-id="ae7a0-214">activo de variable de saludo con suscripción de hello Id. a continuación, se recupera con **Get-AutomationVariable** y suscripción Hola establecido con **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-214">hello variable asset with hello subscription ID is then retrieved with **Get-AutomationVariable** and hello subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="ae7a0-215">Get VMs</span><span class="sxs-lookup"><span data-stu-id="ae7a0-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="ae7a0-216">**Get-AzureVM** es tooretrieve usado Hola Hola runbook funcionará con las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-216">**Get-AzureVM** is used tooretrieve hello virtual machines hello runbook will work with.</span></span>  <span data-ttu-id="ae7a0-217">Si se proporciona un valor en hello **ServiceName** variable, sólo hello las máquinas virtuales con ese nombre de servicio se recuperan de entrada.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-217">If a value is provided in hello **ServiceName** input variable, then only hello virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="ae7a0-218">Si **ServiceName** está vacío, se recuperan todas las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="ae7a0-219">Inicio o detención de máquinas virtuales y envío de resultados</span><span class="sxs-lookup"><span data-stu-id="ae7a0-219">Start/Stop virtual machines and send output</span></span>
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="ae7a0-220">en las líneas siguientes Hola paso a paso a través de cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-220">hello next lines step through each virtual machine.</span></span>  <span data-ttu-id="ae7a0-221">En primer lugar Hola **PowerState** de hello máquina virtual está activado toosee si ya está en ejecución o detenido, dependen de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-221">First hello **PowerState** of hello virtual machine is checked toosee if it is already running or stopped, depending on hello runbook.</span></span>  <span data-ttu-id="ae7a0-222">Si ya está en estado de destino de hello, se envía un mensaje toooutput y Hola runbook finaliza.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-222">If it is already in hello target state, then a message is sent toooutput, and hello runbook ends.</span></span>  <span data-ttu-id="ae7a0-223">Si no es así, a continuación, **Start-AzureVM** o **Stop-AzureVM** es tooattempt usado toostart o detener Hola máquina virtual con el resultado de hello de variable de hello solicitud tooa almacenado.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used tooattempt toostart or stop hello virtual machine with hello result of hello request stored tooa variable.</span></span>  <span data-ttu-id="ae7a0-224">Se envía un mensaje, a continuación, especificar toooutput si toostart de solicitud de Hola o detención se envió correctamente.</span><span class="sxs-lookup"><span data-stu-id="ae7a0-224">A message is then sent toooutput specifying whether hello request toostart or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae7a0-225">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ae7a0-225">Next steps</span></span>
* <span data-ttu-id="ae7a0-226">toolearn más acerca de cómo trabajar con runbooks secundarios, vea [runbooks secundarios en automatización de Azure](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="ae7a0-226">toolearn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="ae7a0-227">solucionar problemas de mensajes durante la ejecución de un runbook y toohelp de registro de salida de toolearn más información sobre, consulte [Runbook salida y mensajes en automatización de Azure](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="ae7a0-227">toolearn more about output messages during runbook execution and logging toohelp troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

