---
title: "Recopilación de datos de Log Analytics con un runbook en Azure Automation | Microsoft Docs"
description: "Tutorial paso a paso que le guía en la creación de un runbook en Azure Automation para recopilar datos en el repositorio de OMS y analizarlos en Log Analytics."
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
ms.openlocfilehash: 59f674c9c6404da7f5384539189f41a4ba1a939a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="a26d1-103">Recopilación de datos de Log Analytics con un runbook de Azure Automation</span><span class="sxs-lookup"><span data-stu-id="a26d1-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="a26d1-104">Puede recopilar una cantidad significativa de datos en Log Analytics desde diversos orígenes como son los [orígenes de datos](../log-analytics/log-analytics-data-sources.md) de agentes y también los [datos recopilados de Azure](../log-analytics/log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="a26d1-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="a26d1-105">Sin embargo, hay un escenario en el que es necesario recopilar datos que no son accesibles a través de estos orígenes estándar.</span><span class="sxs-lookup"><span data-stu-id="a26d1-105">There are a scenarios though where you need to collect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="a26d1-106">Puede usar [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) para escribir los datos de Log Analytics desde cualquier cliente de API de REST.</span><span class="sxs-lookup"><span data-stu-id="a26d1-106">In these cases, you can use the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) to write data to Log Analytics from any REST API client.</span></span>  <span data-ttu-id="a26d1-107">Un método común para realizar esta recopilación de datos es usar un runbook en Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="a26d1-107">A common method to perform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="a26d1-108">Este tutorial le guía a través del proceso para crear y programar un runbook en Azure Automation para escribir datos en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a26d1-108">This tutorial walks through the process for creating and scheduling a runbook in Azure Automation to write data to Log Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a26d1-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a26d1-109">Prerequisites</span></span>
<span data-ttu-id="a26d1-110">Este escenario requiere los siguientes recursos configurados en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a26d1-110">This scenario requires the following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="a26d1-111">Ambos pueden ser una cuenta gratuita.</span><span class="sxs-lookup"><span data-stu-id="a26d1-111">Both can be a free account.</span></span>

- <span data-ttu-id="a26d1-112">[Área de trabajo de Log Analytics](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a26d1-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="a26d1-113">[Cuenta de Azure Automation](../automation/automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a26d1-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="a26d1-114">Información general del escenario</span><span class="sxs-lookup"><span data-stu-id="a26d1-114">Overview of scenario</span></span>
<span data-ttu-id="a26d1-115">En este tutorial, escribirá un runbook que recopila información acerca de los trabajos de Automation.</span><span class="sxs-lookup"><span data-stu-id="a26d1-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="a26d1-116">Los runbooks de Azure Automation se implementan con PowerShell, de modo que podrá empezar por escribir y probar un script en el editor de Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="a26d1-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in the Azure Automation editor.</span></span>  <span data-ttu-id="a26d1-117">Cuando haya comprobado que está recopilando la información necesaria, escribirá los datos en Log Analytics y comprobará el tipo de datos personalizado.</span><span class="sxs-lookup"><span data-stu-id="a26d1-117">Once you verify that you're collecting the required information, you'll write that data to Log Analytics and verify the custom data type.</span></span>  <span data-ttu-id="a26d1-118">Finalmente, creará una programación para iniciar el runbook a intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="a26d1-118">Finally, you'll create a schedule to start the runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="a26d1-119">Puede configurar Azure Automation para enviar información de trabajos a Log Analytics sin este runbook.</span><span class="sxs-lookup"><span data-stu-id="a26d1-119">You can configure Azure Automation to send job information to Log Analytics without this runbook.</span></span>  <span data-ttu-id="a26d1-120">Este escenario se usa principalmente para el tutorial y se recomienda enviar los datos a un área de trabajo de prueba.</span><span class="sxs-lookup"><span data-stu-id="a26d1-120">This scenario is primarily used to support the tutorial, and it's recommended that you send the data to a test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="a26d1-121">1. Instalación del módulo Data Collector API</span><span class="sxs-lookup"><span data-stu-id="a26d1-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="a26d1-122">Cada [solicitud de HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) debe tener el formato adecuado e incluir un encabezado de autorización.</span><span class="sxs-lookup"><span data-stu-id="a26d1-122">Every [request from the HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="a26d1-123">Puede hacer esto en el runbook, aunque puede reducir la cantidad de código necesario con un módulo que simplifica este proceso.</span><span class="sxs-lookup"><span data-stu-id="a26d1-123">You can do this in your runbook, but you can reduce the amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="a26d1-124">Uno de los módulos que puede usar es [OMSIngestionAPI](https://www.powershellgallery.com/packages/OMSIngestionAPI) en la Galería de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a26d1-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in the PowerShell Gallery.</span></span>

<span data-ttu-id="a26d1-125">Para usar un [módulo](../automation/automation-integration-modules.md) en un runbook, debe estar instalado en su cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="a26d1-125">To use a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="a26d1-126">Cualquier runbook de la misma cuenta puede utilizar entonces las funciones del módulo.</span><span class="sxs-lookup"><span data-stu-id="a26d1-126">Any runbook in the same account can then use the functions in the module.</span></span>  <span data-ttu-id="a26d1-127">Puede instalar un nuevo módulo seleccionando **Activos** > **Módulos** > **Agregar un módulo** en su cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="a26d1-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="a26d1-128">Sin embargo, la Galería de PowerShell le ofrece una opción rápida para implementar un módulo directamente en su cuenta de Automation, de modo que puede usar esa opción para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a26d1-128">The PowerShell Gallery though gives you a quick option to deploy a module directly to your automation account so you can use that option for this tutorial.</span></span>  

![Módulo OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="a26d1-130">Vaya a la [Galería de PowerShell](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="a26d1-130">Go to [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="a26d1-131">Busque **OMSIngestionAPI**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="a26d1-132">Haga clic en el botón **Deploy to Azure Automation** (Implementar en Azure Automation).</span><span class="sxs-lookup"><span data-stu-id="a26d1-132">Click on the **Deploy to Azure Automation** button.</span></span>
4. <span data-ttu-id="a26d1-133">Seleccione su cuenta de Automation y haga clic en **Aceptar** para instalar el módulo.</span><span class="sxs-lookup"><span data-stu-id="a26d1-133">Select your automation account and click **OK** to install the module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="a26d1-134">2. Creación de las variables de Automation</span><span class="sxs-lookup"><span data-stu-id="a26d1-134">2. Create Automation variables</span></span>
<span data-ttu-id="a26d1-135">[Las variables de Automation](..\automation\automation-variables.md) contienen valores que pueden usarse en todos los runbooks en su cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="a26d1-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="a26d1-136">Hacen que los runbooks sean más flexibles, ya que permiten cambiar estos valores sin necesidad de modificar el runbook real.</span><span class="sxs-lookup"><span data-stu-id="a26d1-136">They make runbooks more flexible by allowing you to change these values without editing the actual runbook.</span></span> <span data-ttu-id="a26d1-137">Cada solicitud de HTTP Data Collector API requiere el identificador y la clave del área de trabajo de OMS y los recursos de variable son ideales para almacenar esta información.</span><span class="sxs-lookup"><span data-stu-id="a26d1-137">Every request from the HTTP Data Collector API requires the ID and key of the OMS workspace, and variable assets are ideal to store this information.</span></span>  

![Variables](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="a26d1-139">En Azure Portal, vaya a su cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="a26d1-139">In the Azure portal, navigate to your Automation account.</span></span>
2. <span data-ttu-id="a26d1-140">Seleccione **Variables** en **Recursos compartidos**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="a26d1-141">Haga clic en **Agregar una variable** y cree las dos variables en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="a26d1-141">Click **Add a variable** and create the two variables in the following table.</span></span>

| <span data-ttu-id="a26d1-142">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a26d1-142">Property</span></span> | <span data-ttu-id="a26d1-143">Valor de identificador de área de trabajo</span><span class="sxs-lookup"><span data-stu-id="a26d1-143">Workspace ID Value</span></span> | <span data-ttu-id="a26d1-144">Valor de clave de área de trabajo</span><span class="sxs-lookup"><span data-stu-id="a26d1-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a26d1-145">Nombre</span><span class="sxs-lookup"><span data-stu-id="a26d1-145">Name</span></span> | <span data-ttu-id="a26d1-146">WorkspaceId</span><span class="sxs-lookup"><span data-stu-id="a26d1-146">WorkspaceId</span></span> | <span data-ttu-id="a26d1-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="a26d1-147">WorkspaceKey</span></span> |
| <span data-ttu-id="a26d1-148">Tipo</span><span class="sxs-lookup"><span data-stu-id="a26d1-148">Type</span></span> | <span data-ttu-id="a26d1-149">String</span><span class="sxs-lookup"><span data-stu-id="a26d1-149">String</span></span> | <span data-ttu-id="a26d1-150">String</span><span class="sxs-lookup"><span data-stu-id="a26d1-150">String</span></span> |
| <span data-ttu-id="a26d1-151">Valor</span><span class="sxs-lookup"><span data-stu-id="a26d1-151">Value</span></span> | <span data-ttu-id="a26d1-152">Pegue el identificador de área de trabajo de su área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a26d1-152">Paste in the Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="a26d1-153">Pegue la clave secundaria o principal de su área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a26d1-153">Paste in with the Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="a26d1-154">Cifrados</span><span class="sxs-lookup"><span data-stu-id="a26d1-154">Encrypted</span></span> | <span data-ttu-id="a26d1-155">No</span><span class="sxs-lookup"><span data-stu-id="a26d1-155">No</span></span> | <span data-ttu-id="a26d1-156">Sí</span><span class="sxs-lookup"><span data-stu-id="a26d1-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="a26d1-157">3. Creación de runbook</span><span class="sxs-lookup"><span data-stu-id="a26d1-157">3. Create runbook</span></span>

<span data-ttu-id="a26d1-158">Azure Automation tiene un editor en el portal donde puede editar y probar el runbook.</span><span class="sxs-lookup"><span data-stu-id="a26d1-158">Azure Automation has an editor in the portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="a26d1-159">Tiene la opción de usar el editor de scripts para trabajar con [PowerShell directamente](../automation/automation-edit-textual-runbook.md) o [crear un runbook gráfico](../automation/automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="a26d1-159">You have the option to use the script editor to work with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="a26d1-160">En este tutorial, trabajará con un script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a26d1-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Edición de un runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="a26d1-162">Vaya a su cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="a26d1-162">Navigate to your Automation account.</span></span>  
2. <span data-ttu-id="a26d1-163">Haga clic en **Runbooks** > **Agregar un runbook** > **Crear un nuevo runbook**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="a26d1-164">Como nombre del runbook, escriba **Collect-Automation-jobs**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-164">For the runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="a26d1-165">Como tipo de runbook, seleccione **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-165">For the runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="a26d1-166">Haga clic en **Crear** para crear el runbook e inicie el editor.</span><span class="sxs-lookup"><span data-stu-id="a26d1-166">Click **Create** to create the runbook and start the editor.</span></span>
5. <span data-ttu-id="a26d1-167">Copie y pegue el código siguiente en el runbook.</span><span class="sxs-lookup"><span data-stu-id="a26d1-167">Copy and paste the following code into the runbook.</span></span>  <span data-ttu-id="a26d1-168">Consulte los comentarios en el script para ver una explicación del código.</span><span class="sxs-lookup"><span data-stu-id="a26d1-168">Refer to the comments in the script for explanation of the code.</span></span>
    
        # Get information required for the automation account from parameter values when the runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate to the Automation account using the Azure connection created when the Automation account was created.
        # Code copied from the runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set the $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set the name of the record type.
        $logType = "AutomationJob"
        
        # Get the jobs from the past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert the job data to json
            $body = $jobs | ConvertTo-Json
        
            # Write the body to verbose output so we can inspect it if verbose logging is on for the runbook.
            Write-Verbose $body
        
            # Send the data to Log Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="a26d1-169">4. Prueba del runbook</span><span class="sxs-lookup"><span data-stu-id="a26d1-169">4. Test runbook</span></span>
<span data-ttu-id="a26d1-170">Azure Automation incluye un entorno para [probar el runbook](../automation/automation-testing-runbook.md) antes de publicarlo.</span><span class="sxs-lookup"><span data-stu-id="a26d1-170">Azure Automation includes an environment to [test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="a26d1-171">Puede inspeccionar los datos recopilados por el runbook y comprobar que escribe en Log Analytics según lo previsto antes de publicarlo para producción.</span><span class="sxs-lookup"><span data-stu-id="a26d1-171">You can inspect the data collected by the runbook and verify that it writes to Log Analytics as expected before publishing it to production.</span></span> 
 
![Prueba del runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="a26d1-173">Haga clic en **Guardar** para guardar el runbook.</span><span class="sxs-lookup"><span data-stu-id="a26d1-173">Click **Save** to save the runbook.</span></span>
1. <span data-ttu-id="a26d1-174">Haga clic en **Panel de prueba** para abrir el runbook en el entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a26d1-174">Click **Test pane** to open the runbook in the test environment.</span></span>
3. <span data-ttu-id="a26d1-175">Puesto que el runbook tiene parámetros, se le pedirá que escriba sus valores.</span><span class="sxs-lookup"><span data-stu-id="a26d1-175">Since your runbook has parameters, you're prompted to enter values for them.</span></span>  <span data-ttu-id="a26d1-176">Escriba el nombre del grupo de recursos y la cuenta de Automation desde los que va a recopilar la información de los trabajos.</span><span class="sxs-lookup"><span data-stu-id="a26d1-176">Enter the name of the resource group and the automation account that your going to collect job information from.</span></span>
4. <span data-ttu-id="a26d1-177">Haga clic en **Iniciar** para iniciar el runbook.</span><span class="sxs-lookup"><span data-stu-id="a26d1-177">Click **Start** to the start the runbook.</span></span>
3. <span data-ttu-id="a26d1-178">Se iniciará el runbook con el estado **En cola** antes de pasar a **En ejecución**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-178">The runbook will start with a status of **Queued** before it goes to **Running**.</span></span>  
3. <span data-ttu-id="a26d1-179">El runbook debe mostrar una salida detallada con los trabajos recopilados en formato json.</span><span class="sxs-lookup"><span data-stu-id="a26d1-179">The runbook should display verbose output with the jobs collected in json format.</span></span>  <span data-ttu-id="a26d1-180">Si no aparece ningún trabajo, puede que no se haya creado ninguno en la cuenta de Automation en la última hora.</span><span class="sxs-lookup"><span data-stu-id="a26d1-180">If no jobs are listed, then there may have been no jobs created in the automation account in the last hour.</span></span>  <span data-ttu-id="a26d1-181">Pruebe a iniciar un runbook en la cuenta de Automation y, a continuación, vuelva a realizar la prueba.</span><span class="sxs-lookup"><span data-stu-id="a26d1-181">Try starting any runbook in the automation account and then perform the test again.</span></span>
4. <span data-ttu-id="a26d1-182">Asegúrese de que el resultado no muestra ningún error en el comando de registro de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a26d1-182">Ensure that the output doesn't show any errors in the post command to Log Analytics.</span></span>  <span data-ttu-id="a26d1-183">Debería ver un mensaje similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="a26d1-183">You should have a message similar to the following.</span></span>

    ![Registro de salida](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="a26d1-185">5. Comprobación de los registros de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="a26d1-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="a26d1-186">Una vez que el runbook ha completado la prueba y se ha comprobado que la salida se ha recibido correctamente, puede comprobar que los registros se crearon mediante una [búsqueda de registros de Log Analytics](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="a26d1-186">Once the runbook has completed in test, and you verified that the output was successfully received, you can verify that the records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![Resultados del registro](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="a26d1-188">En Azure Portal, seleccione el área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a26d1-188">In the Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="a26d1-189">Haga clic en **Búsqueda de registros**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="a26d1-190">Escriba el siguiente comando `Type=AutomationJob_CL` y haga clic en el botón de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="a26d1-190">Type the following command `Type=AutomationJob_CL` and click the search button.</span></span> <span data-ttu-id="a26d1-191">Tenga en cuenta que el tipo de registro incluye _CL, que no se especifica en el script.</span><span class="sxs-lookup"><span data-stu-id="a26d1-191">Note that the record type includes _CL that isn't specified in the script.</span></span>  <span data-ttu-id="a26d1-192">Dicho sufijo se anexa automáticamente al tipo de registro para indicar que es un tipo de registro personalizado.</span><span class="sxs-lookup"><span data-stu-id="a26d1-192">That suffix is automatically appended to the log type to indicate that it's a custom log type.</span></span>
4. <span data-ttu-id="a26d1-193">Debería ver que uno o varios de los registros devueltos indican que el runbook funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="a26d1-193">You should see one or more records returned indicating that the runbook is working as expected.</span></span>


## <a name="6-publish-the-runbook"></a><span data-ttu-id="a26d1-194">6. Publicación del runbook</span><span class="sxs-lookup"><span data-stu-id="a26d1-194">6. Publish the runbook</span></span>
<span data-ttu-id="a26d1-195">Una vez que haya comprobado que el runbook funciona correctamente, debe publicarlo para que pueda ejecutarse en un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a26d1-195">Once you've verified that the runbook is working correctly, you need to publish it so you can run it in production.</span></span>  <span data-ttu-id="a26d1-196">Puede seguir editando y probando el runbook sin modificar la versión publicada.</span><span class="sxs-lookup"><span data-stu-id="a26d1-196">You can continue to edit and test the runbook without modifying the published version.</span></span>  

![Publicación del runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="a26d1-198">Vuelva a su cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="a26d1-198">Return to your automation account.</span></span>
2. <span data-ttu-id="a26d1-199">Haga clic en **Runbooks** y seleccione **Collect-Automation-jobs**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="a26d1-200">Haga clic en **Editar** y, a continuación, en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="a26d1-201">Haga clic en **Sí** cuando se le pida que confirme que desea sobrescribir la versión publicada previamente.</span><span class="sxs-lookup"><span data-stu-id="a26d1-201">Click **Yes** when asked to verify that you want to overwrite the previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="a26d1-202">7. Establecimiento de las opciones de registro</span><span class="sxs-lookup"><span data-stu-id="a26d1-202">7. Set logging options</span></span> 
<span data-ttu-id="a26d1-203">Para la prueba, podía ver la [salida detallada](../automation/automation-runbook-output-and-messages.md#message-streams) porque estableció la variable $VerbosePreference en el script.</span><span class="sxs-lookup"><span data-stu-id="a26d1-203">For test, you were able to view [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set the $VerbosePreference variable in the script.</span></span>  <span data-ttu-id="a26d1-204">En entornos de producción, si desea ver una salida detallada, debe establecer las propiedades de registro del runbook.</span><span class="sxs-lookup"><span data-stu-id="a26d1-204">For production, you need to set the logging properties for the runbook if you want to view verbose output.</span></span>  <span data-ttu-id="a26d1-205">Para el runbook usado en este tutorial, se mostrarán los datos json que se envían a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a26d1-205">For the runbook used in this tutorial, this will display the json data being sent to Log Analytics.</span></span>

![Registro y seguimiento](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="a26d1-207">En las propiedades del runbook, seleccione **Registro y seguimiento** en **Configuración de runbook**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-207">In the properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="a26d1-208">Cambie la configuración de **Registrar registros detallados** a **Activado**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-208">Change the setting for **Log verbose records** to **On**.</span></span>
3. <span data-ttu-id="a26d1-209">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="a26d1-210">8. Programación de un runbook</span><span class="sxs-lookup"><span data-stu-id="a26d1-210">8. Schedule runbook</span></span>
<span data-ttu-id="a26d1-211">La manera más común de iniciar un runbook que recopila datos de supervisión es programarlo para que se ejecute automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a26d1-211">The most common way to start a runbook that collects monitoring data is to schedule it to run automatically.</span></span>  <span data-ttu-id="a26d1-212">Para ello, debe crear una [programación en Azure Automation](../automation/automation-schedules.md) y asociarla al runbook.</span><span class="sxs-lookup"><span data-stu-id="a26d1-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it to your runbook.</span></span>

![Programación de un runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="a26d1-214">En las propiedades del runbook, seleccione **Programaciones** en **Recursos**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-214">In the properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="a26d1-215">Haga clic en **Agregar una programación** > **Vincular una programación a su runbook** > **Crear una nueva programación**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-215">Click **Add a schedule** > **Link a schedule to your runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="a26d1-216">Escriba los valores siguientes para la programación y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-216">Type in the following values for the schedule and click **Create**.</span></span>

| <span data-ttu-id="a26d1-217">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a26d1-217">Property</span></span> | <span data-ttu-id="a26d1-218">Valor</span><span class="sxs-lookup"><span data-stu-id="a26d1-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="a26d1-219">Nombre</span><span class="sxs-lookup"><span data-stu-id="a26d1-219">Name</span></span> | <span data-ttu-id="a26d1-220">AutomationJobs-Hourly</span><span class="sxs-lookup"><span data-stu-id="a26d1-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="a26d1-221">Se inicia</span><span class="sxs-lookup"><span data-stu-id="a26d1-221">Starts</span></span> | <span data-ttu-id="a26d1-222">Seleccione cualquier hora al menos 5 minutos después de la hora actual.</span><span class="sxs-lookup"><span data-stu-id="a26d1-222">Select any time at least 5 minutes past the current time.</span></span> |
| <span data-ttu-id="a26d1-223">Periodicidad</span><span class="sxs-lookup"><span data-stu-id="a26d1-223">Recurrence</span></span> | <span data-ttu-id="a26d1-224">Periódica</span><span class="sxs-lookup"><span data-stu-id="a26d1-224">Recurring</span></span> |
| <span data-ttu-id="a26d1-225">Repetir cada</span><span class="sxs-lookup"><span data-stu-id="a26d1-225">Recur every</span></span> | <span data-ttu-id="a26d1-226">1 hora</span><span class="sxs-lookup"><span data-stu-id="a26d1-226">1 hour</span></span> |
| <span data-ttu-id="a26d1-227">Configurar expiración</span><span class="sxs-lookup"><span data-stu-id="a26d1-227">Set expiration</span></span> | <span data-ttu-id="a26d1-228">No</span><span class="sxs-lookup"><span data-stu-id="a26d1-228">No</span></span> |

<span data-ttu-id="a26d1-229">Una vez creada la programación, debe establecer los valores de los parámetros que se usarán cada vez que esta inicie el runbook.</span><span class="sxs-lookup"><span data-stu-id="a26d1-229">Once the schedule is created, you need to set the parameter values that will be used each time this schedule starts the runbook.</span></span>

6. <span data-ttu-id="a26d1-230">Haga clic en **Configurar parámetros y ejecutar configuraciones**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="a26d1-231">Rellene los valores de **ResourceGroupName** y **AutomationAccountName**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="a26d1-232">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="a26d1-233">9. Comprobación de que el runbook se inicia según la programación</span><span class="sxs-lookup"><span data-stu-id="a26d1-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="a26d1-234">Siempre que se inicia un runbook, [se crea un trabajo](../automation/automation-runbook-execution.md) y se registran sus resultados.</span><span class="sxs-lookup"><span data-stu-id="a26d1-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="a26d1-235">De hecho, son los mismos trabajos que el runbook recopila.</span><span class="sxs-lookup"><span data-stu-id="a26d1-235">In fact, these are the same jobs that the runbook is collecting.</span></span>  <span data-ttu-id="a26d1-236">Puede verificar que el runbook se inicia como se esperaba comprobando los trabajos del runbook una vez que haya pasado la hora de inicio de la programación.</span><span class="sxs-lookup"><span data-stu-id="a26d1-236">You can verify that the runbook starts as expected by checking the jobs for the runbook after the start time for the schedule has passed.</span></span>

![Trabajos](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="a26d1-238">En las propiedades del runbook, seleccione **Trabajos** en **Recursos**.</span><span class="sxs-lookup"><span data-stu-id="a26d1-238">In the properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="a26d1-239">Debería ver una lista de trabajos de cada vez que se inició el runbook.</span><span class="sxs-lookup"><span data-stu-id="a26d1-239">You should see a listing of jobs for each time the runbook was started.</span></span>
3. <span data-ttu-id="a26d1-240">Haga clic en uno de los trabajos para ver sus detalles.</span><span class="sxs-lookup"><span data-stu-id="a26d1-240">Click on one of the jobs to view its details.</span></span>
4. <span data-ttu-id="a26d1-241">Haga clic en **Todos los registros** para ver los registros y la salida del runbook.</span><span class="sxs-lookup"><span data-stu-id="a26d1-241">Click on **All logs** to view the logs and output from the runbook.</span></span>
5. <span data-ttu-id="a26d1-242">Desplácese hacia abajo para buscar una entrada similar a la de la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="a26d1-242">Scroll to the bottom to find an entry similar to the image below.</span></span><br>![Detallado](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="a26d1-244">Haga clic en esta entrada para ver los datos de json detallados que se enviaron a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a26d1-244">Click on this entry to view the detailed json data  that was sent to Log Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="a26d1-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a26d1-245">Next steps</span></span>
- <span data-ttu-id="a26d1-246">Use el [Diseñador de vistas](../log-analytics/log-analytics-view-designer.md) para crear una vista que muestre los datos que se han recopilado en el repositorio de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a26d1-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) to create a view displaying the data that you've collected to the Log Analytics repository.</span></span>
- <span data-ttu-id="a26d1-247">Empaquete el runbook en una [solución de administración](operations-management-suite-solutions-creating.md) para distribuirla a los clientes.</span><span class="sxs-lookup"><span data-stu-id="a26d1-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) to distribute to customers.</span></span>
- <span data-ttu-id="a26d1-248">Más información sobre [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="a26d1-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="a26d1-249">Más información sobre [Azure Automation](https://docs.microsoft.com/azure/automation/).</span><span class="sxs-lookup"><span data-stu-id="a26d1-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="a26d1-250">Más información sobre la [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span><span class="sxs-lookup"><span data-stu-id="a26d1-250">Learn more about the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>