---
title: "aaaCollecting datos de análisis de registros con un runbook en automatización de Azure | Documentos de Microsoft"
description: "Tutorial paso a paso le guía por la creación de un runbook en datos de toocollect de automatización de Azure en el repositorio de OMS de hello para el análisis por análisis de registros."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="df25c-103">Recopilación de datos de Log Analytics con un runbook de Azure Automation</span><span class="sxs-lookup"><span data-stu-id="df25c-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="df25c-104">Puede recopilar una cantidad significativa de datos en Log Analytics desde diversos orígenes como son los [orígenes de datos](../log-analytics/log-analytics-data-sources.md) de agentes y también los [datos recopilados de Azure](../log-analytics/log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="df25c-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="df25c-105">Hay un escenarios aunque donde debe toocollect datos que no es accesible a través de estos orígenes estándares.</span><span class="sxs-lookup"><span data-stu-id="df25c-105">There are a scenarios though where you need toocollect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="df25c-106">En estos casos, puede usar hello [API de recopilador de datos HTTP](../log-analytics/log-analytics-data-collector-api.md) toowrite datos tooLog análisis desde cualquier cliente de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="df25c-106">In these cases, you can use hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) toowrite data tooLog Analytics from any REST API client.</span></span>  <span data-ttu-id="df25c-107">Un tooperform método común esta recopilación de datos está usando un runbook en automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="df25c-107">A common method tooperform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="df25c-108">Este tutorial le guía a través del proceso de Hola para crear y programar un runbook en automatización de Azure toowrite datos tooLog análisis.</span><span class="sxs-lookup"><span data-stu-id="df25c-108">This tutorial walks through hello process for creating and scheduling a runbook in Azure Automation toowrite data tooLog Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="df25c-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="df25c-109">Prerequisites</span></span>
<span data-ttu-id="df25c-110">Este escenario requiere Hola siguiendo los recursos configurados en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="df25c-110">This scenario requires hello following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="df25c-111">Ambos pueden ser una cuenta gratuita.</span><span class="sxs-lookup"><span data-stu-id="df25c-111">Both can be a free account.</span></span>

- <span data-ttu-id="df25c-112">[Área de trabajo de Log Analytics](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="df25c-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="df25c-113">[Cuenta de Azure Automation](../automation/automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="df25c-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="df25c-114">Información general del escenario</span><span class="sxs-lookup"><span data-stu-id="df25c-114">Overview of scenario</span></span>
<span data-ttu-id="df25c-115">En este tutorial, escribirá un runbook que recopila información acerca de los trabajos de Automation.</span><span class="sxs-lookup"><span data-stu-id="df25c-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="df25c-116">Runbooks de automatización de Azure se implementan con PowerShell, por lo que podrá empezar por escribir y probar una secuencia de comandos en el editor de automatización de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="df25c-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in hello Azure Automation editor.</span></span>  <span data-ttu-id="df25c-117">Cuando haya comprobado que está recopilando información de hello necesario, podrá escribir ese tooLog análisis de datos y comprobar el tipo de datos personalizados de Hola.</span><span class="sxs-lookup"><span data-stu-id="df25c-117">Once you verify that you're collecting hello required information, you'll write that data tooLog Analytics and verify hello custom data type.</span></span>  <span data-ttu-id="df25c-118">Por último, creará un runbook de programación toostart Hola a intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="df25c-118">Finally, you'll create a schedule toostart hello runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="df25c-119">Puede configurar la automatización de Azure toosend trabajo información tooLog análisis sin este runbook.</span><span class="sxs-lookup"><span data-stu-id="df25c-119">You can configure Azure Automation toosend job information tooLog Analytics without this runbook.</span></span>  <span data-ttu-id="df25c-120">Este escenario es principalmente el tutorial de hello toosupport usado y se recomienda que enviar el área de trabajo de hello datos tooa prueba.</span><span class="sxs-lookup"><span data-stu-id="df25c-120">This scenario is primarily used toosupport hello tutorial, and it's recommended that you send hello data tooa test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="df25c-121">1. Instalación del módulo Data Collector API</span><span class="sxs-lookup"><span data-stu-id="df25c-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="df25c-122">Cada [solicitud de API de recopilador de datos HTTP hello](../log-analytics/log-analytics-data-collector-api.md#create-a-request) debe tener el formato adecuado e incluir un encabezado de autorización.</span><span class="sxs-lookup"><span data-stu-id="df25c-122">Every [request from hello HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="df25c-123">Para hacer esto en su runbook, pero se puede reducir la cantidad de Hola de código necesario, con un módulo que simplifica este proceso.</span><span class="sxs-lookup"><span data-stu-id="df25c-123">You can do this in your runbook, but you can reduce hello amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="df25c-124">Es un módulo que puede usar [OMSIngestionAPI módulo](https://www.powershellgallery.com/packages/OMSIngestionAPI) Hola Galería de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="df25c-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in hello PowerShell Gallery.</span></span>

<span data-ttu-id="df25c-125">toouse una [módulo](../automation/automation-integration-modules.md) en un runbook, debe instalarse en su cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="df25c-125">toouse a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="df25c-126">Funciones de módulo de Hola Hola a cualquier runbook Hola, a continuación, puede usar la misma cuenta.</span><span class="sxs-lookup"><span data-stu-id="df25c-126">Any runbook in hello same account can then use hello functions in hello module.</span></span>  <span data-ttu-id="df25c-127">Puede instalar un nuevo módulo seleccionando **Activos** > **Módulos** > **Agregar un módulo** en su cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="df25c-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="df25c-128">Hola Galería de PowerShell aunque le ofrece una toodeploy opciones rápidas un módulo directamente tooyour automatización de la cuenta para poder utilizar esta opción para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="df25c-128">hello PowerShell Gallery though gives you a quick option toodeploy a module directly tooyour automation account so you can use that option for this tutorial.</span></span>  

![Módulo OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="df25c-130">Vaya demasiado[Galería de PowerShell](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="df25c-130">Go too[PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="df25c-131">Busque **OMSIngestionAPI**.</span><span class="sxs-lookup"><span data-stu-id="df25c-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="df25c-132">Haga clic en hello **implementar tooAzure automatización** botón.</span><span class="sxs-lookup"><span data-stu-id="df25c-132">Click on hello **Deploy tooAzure Automation** button.</span></span>
4. <span data-ttu-id="df25c-133">Seleccione su cuenta de automatización y haga clic en **Aceptar** módulo de hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="df25c-133">Select your automation account and click **OK** tooinstall hello module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="df25c-134">2. Creación de las variables de Automation</span><span class="sxs-lookup"><span data-stu-id="df25c-134">2. Create Automation variables</span></span>
<span data-ttu-id="df25c-135">[Las variables de Automation](..\automation\automation-variables.md) contienen valores que pueden usarse en todos los runbooks en su cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="df25c-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="df25c-136">Realizan runbooks más flexible, ya que permite toochange estos valores sin necesidad de editar Hola runbook real.</span><span class="sxs-lookup"><span data-stu-id="df25c-136">They make runbooks more flexible by allowing you toochange these values without editing hello actual runbook.</span></span> <span data-ttu-id="df25c-137">Requiere que todas las solicitudes de API de recopilador de datos HTTP Hola Hola identificador y la clave de área de trabajo OMS de Hola y activos de variable hay toostore ideal esta información.</span><span class="sxs-lookup"><span data-stu-id="df25c-137">Every request from hello HTTP Data Collector API requires hello ID and key of hello OMS workspace, and variable assets are ideal toostore this information.</span></span>  

![variables](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="df25c-139">Hola portal de Azure, navegue tooyour cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="df25c-139">In hello Azure portal, navigate tooyour Automation account.</span></span>
2. <span data-ttu-id="df25c-140">Seleccione **Variables** en **Recursos compartidos**.</span><span class="sxs-lookup"><span data-stu-id="df25c-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="df25c-141">Haga clic en **agregar una variable** y cree dos variables de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="df25c-141">Click **Add a variable** and create hello two variables in hello following table.</span></span>

| <span data-ttu-id="df25c-142">Propiedad</span><span class="sxs-lookup"><span data-stu-id="df25c-142">Property</span></span> | <span data-ttu-id="df25c-143">Valor de identificador de área de trabajo</span><span class="sxs-lookup"><span data-stu-id="df25c-143">Workspace ID Value</span></span> | <span data-ttu-id="df25c-144">Valor de clave de área de trabajo</span><span class="sxs-lookup"><span data-stu-id="df25c-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="df25c-145">Nombre</span><span class="sxs-lookup"><span data-stu-id="df25c-145">Name</span></span> | <span data-ttu-id="df25c-146">WorkspaceId</span><span class="sxs-lookup"><span data-stu-id="df25c-146">WorkspaceId</span></span> | <span data-ttu-id="df25c-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="df25c-147">WorkspaceKey</span></span> |
| <span data-ttu-id="df25c-148">Tipo</span><span class="sxs-lookup"><span data-stu-id="df25c-148">Type</span></span> | <span data-ttu-id="df25c-149">String</span><span class="sxs-lookup"><span data-stu-id="df25c-149">String</span></span> | <span data-ttu-id="df25c-150">String</span><span class="sxs-lookup"><span data-stu-id="df25c-150">String</span></span> |
| <span data-ttu-id="df25c-151">Valor</span><span class="sxs-lookup"><span data-stu-id="df25c-151">Value</span></span> | <span data-ttu-id="df25c-152">Pegue en hello Id. de área de trabajo del área de trabajo de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="df25c-152">Paste in hello Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="df25c-153">Pegue con hello principal o secundaria de su área de trabajo de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="df25c-153">Paste in with hello Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="df25c-154">Cifrados</span><span class="sxs-lookup"><span data-stu-id="df25c-154">Encrypted</span></span> | <span data-ttu-id="df25c-155">No</span><span class="sxs-lookup"><span data-stu-id="df25c-155">No</span></span> | <span data-ttu-id="df25c-156">Sí</span><span class="sxs-lookup"><span data-stu-id="df25c-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="df25c-157">3. Creación de runbook</span><span class="sxs-lookup"><span data-stu-id="df25c-157">3. Create runbook</span></span>

<span data-ttu-id="df25c-158">Automatización de Azure tiene un editor en el portal de Hola donde puede editar y probar su runbook.</span><span class="sxs-lookup"><span data-stu-id="df25c-158">Azure Automation has an editor in hello portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="df25c-159">Tiene toowork del editor de script de Hola opción toouse Hola con [PowerShell directamente](../automation/automation-edit-textual-runbook.md) o [crear un runbook gráfico](../automation/automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="df25c-159">You have hello option toouse hello script editor toowork with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="df25c-160">En este tutorial, trabajará con un script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="df25c-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Edición de un runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="df25c-162">Navegue tooyour cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="df25c-162">Navigate tooyour Automation account.</span></span>  
2. <span data-ttu-id="df25c-163">Haga clic en **Runbooks** > **Agregar un runbook** > **Crear un nuevo runbook**.</span><span class="sxs-lookup"><span data-stu-id="df25c-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="df25c-164">Nombre de runbook de hello, escriba **trabajos de automatización de recopilar**.</span><span class="sxs-lookup"><span data-stu-id="df25c-164">For hello runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="df25c-165">Para tipo de runbook de hello, seleccione **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="df25c-165">For hello runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="df25c-166">Haga clic en **crear** toocreate Hola runbook e inicio Hola del editor.</span><span class="sxs-lookup"><span data-stu-id="df25c-166">Click **Create** toocreate hello runbook and start hello editor.</span></span>
5. <span data-ttu-id="df25c-167">Copie y pegue Hola siguiente código en hello runbook.</span><span class="sxs-lookup"><span data-stu-id="df25c-167">Copy and paste hello following code into hello runbook.</span></span>  <span data-ttu-id="df25c-168">Consulte toohello comentarios en el script de Hola para ver una explicación del código de hello.</span><span class="sxs-lookup"><span data-stu-id="df25c-168">Refer toohello comments in hello script for explanation of hello code.</span></span>
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="df25c-169">4. Prueba del runbook</span><span class="sxs-lookup"><span data-stu-id="df25c-169">4. Test runbook</span></span>
<span data-ttu-id="df25c-170">Automatización de Azure incluye un entorno demasiado[probar su runbook](../automation/automation-testing-runbook.md) antes de publicarla.</span><span class="sxs-lookup"><span data-stu-id="df25c-170">Azure Automation includes an environment too[test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="df25c-171">Puede inspeccionar los datos de Hola Hola runbook recogidos y compruebe que escribe tooLog análisis según lo esperado antes de publicarlo tooproduction.</span><span class="sxs-lookup"><span data-stu-id="df25c-171">You can inspect hello data collected by hello runbook and verify that it writes tooLog Analytics as expected before publishing it tooproduction.</span></span> 
 
![Prueba del runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="df25c-173">Haga clic en **guardar** toosave Hola runbook.</span><span class="sxs-lookup"><span data-stu-id="df25c-173">Click **Save** toosave hello runbook.</span></span>
1. <span data-ttu-id="df25c-174">Haga clic en **panel prueba** tooopen Hola runbook en el entorno de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="df25c-174">Click **Test pane** tooopen hello runbook in hello test environment.</span></span>
3. <span data-ttu-id="df25c-175">Puesto que el runbook tiene parámetros, le tooenter solicitadas valores para ellos.</span><span class="sxs-lookup"><span data-stu-id="df25c-175">Since your runbook has parameters, you're prompted tooenter values for them.</span></span>  <span data-ttu-id="df25c-176">Escriba Hola nombre del grupo de recursos de Hola y automatización de hello información de la cuenta que su curso toocollect trabajo de.</span><span class="sxs-lookup"><span data-stu-id="df25c-176">Enter hello name of hello resource group and hello automation account that your going toocollect job information from.</span></span>
4. <span data-ttu-id="df25c-177">Haga clic en **iniciar** toohello iniciar runbook Hola.</span><span class="sxs-lookup"><span data-stu-id="df25c-177">Click **Start** toohello start hello runbook.</span></span>
3. <span data-ttu-id="df25c-178">Hola runbook se iniciará con un estado de **en cola** antes de que entre demasiado**ejecutando**.</span><span class="sxs-lookup"><span data-stu-id="df25c-178">hello runbook will start with a status of **Queued** before it goes too**Running**.</span></span>  
3. <span data-ttu-id="df25c-179">Hola runbook debe mostrar un resultado detallado con trabajos de hello recopilados en formato json.</span><span class="sxs-lookup"><span data-stu-id="df25c-179">hello runbook should display verbose output with hello jobs collected in json format.</span></span>  <span data-ttu-id="df25c-180">Si no aparece ningún trabajo, a continuación, no se haya ningún trabajo creado en la cuenta de automatización de Hola Hola última hora.</span><span class="sxs-lookup"><span data-stu-id="df25c-180">If no jobs are listed, then there may have been no jobs created in hello automation account in hello last hour.</span></span>  <span data-ttu-id="df25c-181">Pruebe a iniciar cualquier runbook en la cuenta de automatización de hello y, a continuación, realice pruebas de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="df25c-181">Try starting any runbook in hello automation account and then perform hello test again.</span></span>
4. <span data-ttu-id="df25c-182">Asegúrese de que la salida de hello no muestra que los errores en hello exponer comandos tooLog análisis.</span><span class="sxs-lookup"><span data-stu-id="df25c-182">Ensure that hello output doesn't show any errors in hello post command tooLog Analytics.</span></span>  <span data-ttu-id="df25c-183">Debe tener una continuación toohello similar de mensaje.</span><span class="sxs-lookup"><span data-stu-id="df25c-183">You should have a message similar toohello following.</span></span>

    ![Registro de salida](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="df25c-185">5. Comprobación de los registros de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="df25c-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="df25c-186">Una vez que se ha completado Hola runbook de prueba y haya comprobado que la salida de hello ha sido recibida correctamente, puede comprobar que los registros de Hola se crearon con una [búsqueda de registros de análisis de registros](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="df25c-186">Once hello runbook has completed in test, and you verified that hello output was successfully received, you can verify that hello records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![Resultados del registro](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="df25c-188">Hola portal de Azure, seleccione el área de trabajo de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="df25c-188">In hello Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="df25c-189">Haga clic en **Búsqueda de registros**.</span><span class="sxs-lookup"><span data-stu-id="df25c-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="df25c-190">Hola de tipo siguiente comando `Type=AutomationJob_CL` y haga clic en el botón de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="df25c-190">Type hello following command `Type=AutomationJob_CL` and click hello search button.</span></span> <span data-ttu-id="df25c-191">Tenga en cuenta que el tipo de registro de hello incluye _CL que no se especifica en el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="df25c-191">Note that hello record type includes _CL that isn't specified in hello script.</span></span>  <span data-ttu-id="df25c-192">Ese sufijo es tooindicate de tipo de registro automáticamente anexados toohello que es un tipo de registro personalizado.</span><span class="sxs-lookup"><span data-stu-id="df25c-192">That suffix is automatically appended toohello log type tooindicate that it's a custom log type.</span></span>
4. <span data-ttu-id="df25c-193">Debería ver uno o varios de los registros devueltos que indica que runbook Hola funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="df25c-193">You should see one or more records returned indicating that hello runbook is working as expected.</span></span>


## <a name="6-publish-hello-runbook"></a><span data-ttu-id="df25c-194">6. Publicar Hola runbook</span><span class="sxs-lookup"><span data-stu-id="df25c-194">6. Publish hello runbook</span></span>
<span data-ttu-id="df25c-195">Una vez que haya comprobado que runbook Hola funciona correctamente, necesita toopublish, por lo que puede ejecutar en producción.</span><span class="sxs-lookup"><span data-stu-id="df25c-195">Once you've verified that hello runbook is working correctly, you need toopublish it so you can run it in production.</span></span>  <span data-ttu-id="df25c-196">Puede continuar tooedit y probar Hola runbook sin modificar la versión publicada de Hola.</span><span class="sxs-lookup"><span data-stu-id="df25c-196">You can continue tooedit and test hello runbook without modifying hello published version.</span></span>  

![Publicación del runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="df25c-198">Devolver tooyour cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="df25c-198">Return tooyour automation account.</span></span>
2. <span data-ttu-id="df25c-199">Haga clic en **Runbooks** y seleccione **Collect-Automation-jobs**.</span><span class="sxs-lookup"><span data-stu-id="df25c-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="df25c-200">Haga clic en **Editar** y, a continuación, en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="df25c-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="df25c-201">Haga clic en **Sí** cuando tooverify frecuentes que desea toooverwrite Hola previamente versión publicada.</span><span class="sxs-lookup"><span data-stu-id="df25c-201">Click **Yes** when asked tooverify that you want toooverwrite hello previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="df25c-202">7. Establecimiento de las opciones de registro</span><span class="sxs-lookup"><span data-stu-id="df25c-202">7. Set logging options</span></span> 
<span data-ttu-id="df25c-203">De prueba, era capaz de tooview [resultados detallados](../automation/automation-runbook-output-and-messages.md#message-streams) porque se establece Hola $VerbosePreference variable en el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="df25c-203">For test, you were able tooview [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set hello $VerbosePreference variable in hello script.</span></span>  <span data-ttu-id="df25c-204">Para entornos de producción, debe propiedades de registro de hello tooset de runbook de hello si desea que los resultados detallados de tooview.</span><span class="sxs-lookup"><span data-stu-id="df25c-204">For production, you need tooset hello logging properties for hello runbook if you want tooview verbose output.</span></span>  <span data-ttu-id="df25c-205">Hola runbook usado en este tutorial, se mostrará datos de json de Hola que se envían tooLog análisis.</span><span class="sxs-lookup"><span data-stu-id="df25c-205">For hello runbook used in this tutorial, this will display hello json data being sent tooLog Analytics.</span></span>

![Registro y seguimiento](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="df25c-207">En Propiedades de hello para el runbook seleccione **registro y seguimiento** en **configuración del Runbook**.</span><span class="sxs-lookup"><span data-stu-id="df25c-207">In hello properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="df25c-208">Cambiar configuración de Hola para **registros detallados** demasiado**en**.</span><span class="sxs-lookup"><span data-stu-id="df25c-208">Change hello setting for **Log verbose records** too**On**.</span></span>
3. <span data-ttu-id="df25c-209">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="df25c-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="df25c-210">8. Programación de un runbook</span><span class="sxs-lookup"><span data-stu-id="df25c-210">8. Schedule runbook</span></span>
<span data-ttu-id="df25c-211">Hola toostart de manera más común un runbook que recopila datos de supervisión es tooschedule se toorun automáticamente.</span><span class="sxs-lookup"><span data-stu-id="df25c-211">hello most common way toostart a runbook that collects monitoring data is tooschedule it toorun automatically.</span></span>  <span data-ttu-id="df25c-212">Para ello, crear un [programación en automatización de Azure](../automation/automation-schedules.md) y adjuntar tooyour runbook.</span><span class="sxs-lookup"><span data-stu-id="df25c-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it tooyour runbook.</span></span>

![Programación de un runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="df25c-214">En Propiedades de hello para el runbook, seleccione **programaciones** en **recursos**.</span><span class="sxs-lookup"><span data-stu-id="df25c-214">In hello properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="df25c-215">Haga clic en **agregar una programación** > **vincular un runbook de programación tooyour** > **crear una nueva programación**.</span><span class="sxs-lookup"><span data-stu-id="df25c-215">Click **Add a schedule** > **Link a schedule tooyour runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="df25c-216">Tipo de hello siguientes valores para la programación de Hola y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="df25c-216">Type in hello following values for hello schedule and click **Create**.</span></span>

| <span data-ttu-id="df25c-217">Propiedad</span><span class="sxs-lookup"><span data-stu-id="df25c-217">Property</span></span> | <span data-ttu-id="df25c-218">Valor</span><span class="sxs-lookup"><span data-stu-id="df25c-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="df25c-219">Nombre</span><span class="sxs-lookup"><span data-stu-id="df25c-219">Name</span></span> | <span data-ttu-id="df25c-220">AutomationJobs-Hourly</span><span class="sxs-lookup"><span data-stu-id="df25c-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="df25c-221">Se inicia</span><span class="sxs-lookup"><span data-stu-id="df25c-221">Starts</span></span> | <span data-ttu-id="df25c-222">Seleccione cualquier momento al menos 5 minutos anterior Hola hora actual.</span><span class="sxs-lookup"><span data-stu-id="df25c-222">Select any time at least 5 minutes past hello current time.</span></span> |
| <span data-ttu-id="df25c-223">Periodicidad</span><span class="sxs-lookup"><span data-stu-id="df25c-223">Recurrence</span></span> | <span data-ttu-id="df25c-224">Periódica</span><span class="sxs-lookup"><span data-stu-id="df25c-224">Recurring</span></span> |
| <span data-ttu-id="df25c-225">Repetir cada</span><span class="sxs-lookup"><span data-stu-id="df25c-225">Recur every</span></span> | <span data-ttu-id="df25c-226">1 hora</span><span class="sxs-lookup"><span data-stu-id="df25c-226">1 hour</span></span> |
| <span data-ttu-id="df25c-227">Configurar expiración</span><span class="sxs-lookup"><span data-stu-id="df25c-227">Set expiration</span></span> | <span data-ttu-id="df25c-228">No</span><span class="sxs-lookup"><span data-stu-id="df25c-228">No</span></span> |

<span data-ttu-id="df25c-229">Una vez que se creó la programación de hello, necesita valores de parámetro de hello tooset que se usará cada vez que esta programación inicia runbook Hola.</span><span class="sxs-lookup"><span data-stu-id="df25c-229">Once hello schedule is created, you need tooset hello parameter values that will be used each time this schedule starts hello runbook.</span></span>

6. <span data-ttu-id="df25c-230">Haga clic en **Configurar parámetros y ejecutar configuraciones**.</span><span class="sxs-lookup"><span data-stu-id="df25c-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="df25c-231">Rellene los valores de **ResourceGroupName** y **AutomationAccountName**.</span><span class="sxs-lookup"><span data-stu-id="df25c-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="df25c-232">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="df25c-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="df25c-233">9. Comprobación de que el runbook se inicia según la programación</span><span class="sxs-lookup"><span data-stu-id="df25c-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="df25c-234">Siempre que se inicia un runbook, [se crea un trabajo](../automation/automation-runbook-execution.md) y se registran sus resultados.</span><span class="sxs-lookup"><span data-stu-id="df25c-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="df25c-235">De hecho, se trata de hello está recopilando los mismos trabajos que Hola runbook.</span><span class="sxs-lookup"><span data-stu-id="df25c-235">In fact, these are hello same jobs that hello runbook is collecting.</span></span>  <span data-ttu-id="df25c-236">Puede comprobar que dicho runbook Hola se inicia como se esperaba mediante la comprobación de trabajos de Hola Hola runbook después de que transcurra el tiempo de inicio de Hola para programación Hola.</span><span class="sxs-lookup"><span data-stu-id="df25c-236">You can verify that hello runbook starts as expected by checking hello jobs for hello runbook after hello start time for hello schedule has passed.</span></span>

![Trabajos](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="df25c-238">En Propiedades de hello para el runbook, seleccione **trabajos** en **recursos**.</span><span class="sxs-lookup"><span data-stu-id="df25c-238">In hello properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="df25c-239">Debería ver que una lista de trabajos para cada runbook de Hola de tiempo se inició.</span><span class="sxs-lookup"><span data-stu-id="df25c-239">You should see a listing of jobs for each time hello runbook was started.</span></span>
3. <span data-ttu-id="df25c-240">Haga clic en uno de hello trabajos tooview sus detalles.</span><span class="sxs-lookup"><span data-stu-id="df25c-240">Click on one of hello jobs tooview its details.</span></span>
4. <span data-ttu-id="df25c-241">Haga clic en **todos los registros de** tooview Hola registros y resultados de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="df25c-241">Click on **All logs** tooview hello logs and output from hello runbook.</span></span>
5. <span data-ttu-id="df25c-242">Desplácese toohello inferior toofind una imagen de toohello similar de entrada siguiente.</span><span class="sxs-lookup"><span data-stu-id="df25c-242">Scroll toohello bottom toofind an entry similar toohello image below.</span></span><br>![Detallado](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="df25c-244">Haga clic en esta entrada de datos json que envían tooLog análisis detallados que tooview Hola.</span><span class="sxs-lookup"><span data-stu-id="df25c-244">Click on this entry tooview hello detailed json data  that was sent tooLog Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="df25c-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="df25c-245">Next steps</span></span>
- <span data-ttu-id="df25c-246">Use [Diseñador de vistas](../log-analytics/log-analytics-view-designer.md) Hola de toocreate una vista muestra los datos que ha recopilado toohello repositorio de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="df25c-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) toocreate a view displaying hello data that you've collected toohello Log Analytics repository.</span></span>
- <span data-ttu-id="df25c-247">Empaquetar su runbook en un [solución de administración de](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span><span class="sxs-lookup"><span data-stu-id="df25c-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span></span>
- <span data-ttu-id="df25c-248">Más información sobre [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="df25c-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="df25c-249">Más información sobre [Azure Automation](https://docs.microsoft.com/azure/automation/).</span><span class="sxs-lookup"><span data-stu-id="df25c-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="df25c-250">Obtener más información sobre hello [API de recopilador de datos HTTP](../log-analytics/log-analytics-data-collector-api.md).</span><span class="sxs-lookup"><span data-stu-id="df25c-250">Learn more about hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>
