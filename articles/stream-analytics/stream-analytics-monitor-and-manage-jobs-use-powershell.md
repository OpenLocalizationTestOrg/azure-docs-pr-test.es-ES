---
title: "aaaMonitor y administrar los trabajos de análisis de transmisiones con PowerShell | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomonitor de PowerShell de Azure y los cmdlets de toouse y administrar los trabajos de análisis de transmisiones."
keywords: azure powershell, cmdlets de azure powershell, comando de powershell, scripting de powershell
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="54fb4-104">Supervisar y administrar los trabajos de Análisis de transmisiones con los cmdlets de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="54fb4-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="54fb4-105">Obtenga información acerca de cómo toomonitor y administrar los recursos de análisis de transmisiones con cmdlets de PowerShell de Azure y secuencias de comandos de powershell que se ejecutan las tareas básicas de análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="54fb4-105">Learn how toomonitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="54fb4-106">Requisitos previos para ejecutar cmdlets de Azure PowerShell en Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="54fb4-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="54fb4-107">Cree un grupo de recursos de Azure en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="54fb4-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="54fb4-108">Hola aquí te mostramos una secuencia de comandos de PowerShell de Azure de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="54fb4-108">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="54fb4-109">Para obtener información sobre Azure PowerShell, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="54fb4-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

<span data-ttu-id="54fb4-110">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="54fb4-111">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-111">Azure PowerShell 1.0:</span></span>  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="54fb4-112">Los trabajos de Análisis de transmisiones creados mediante programación no tienen la supervisión habilitada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="54fb4-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="54fb4-113">Puede habilitar la supervisión en hello Azure Portal desplazándose página del Monitor del trabajo toohello manualmente y haga clic en el botón Habilitar de Hola o se puede hacer esto mediante programación siguiendo los pasos de hello ubicados en [análisis de transmisiones de Azure - secuencia de Monitor Análisis de trabajos mediante programación](stream-analytics-monitor-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="54fb4-113">You can manually enable monitoring in hello Azure Portal by navigating toohello job’s Monitor page and clicking hello Enable button or you can do this programmatically by following hello steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="54fb4-114">Cmdlets de PowerShell de Azure en Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="54fb4-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="54fb4-115">Hola siguientes cmdlets de PowerShell de Azure puede ser toomonitor usado y administrar los trabajos de análisis de transmisiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="54fb4-115">hello following Azure PowerShell cmdlets can be used toomonitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="54fb4-116">Tenga en cuenta que Azure PowerShell tiene versiones diferentes.</span><span class="sxs-lookup"><span data-stu-id="54fb4-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="54fb4-117">**En los ejemplos de Hola Hola enumerados primer comando es para Azure PowerShell 0.9.8, segundo comando de hello es para Azure PowerShell 1.0.**</span><span class="sxs-lookup"><span data-stu-id="54fb4-117">**In hello examples listed hello first command is for Azure PowerShell 0.9.8, hello second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="54fb4-118">comandos de Hello Azure PowerShell 1.0 siempre tendrá "AzureRM" en el comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="54fb4-118">hello Azure PowerShell 1.0 commands will always have "AzureRM" in hello command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="54fb4-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="54fb4-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="54fb4-120">Obtiene información sobre el trabajo sobre un trabajo específico dentro de un grupo de recursos o muestra todos los trabajos de análisis de transmisiones definidos en la suscripción de Azure de Hola o grupo de recursos especificado.</span><span class="sxs-lookup"><span data-stu-id="54fb4-120">Lists all Stream Analytics jobs defined in hello Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="54fb4-121">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="54fb4-121">**Example 1**</span></span>

<span data-ttu-id="54fb4-122">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="54fb4-123">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="54fb4-124">Este comando de PowerShell devuelve información acerca de todos los trabajos de análisis de transmisiones de Hola Hola suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="54fb4-124">This PowerShell command returns information about all hello Stream Analytics jobs in hello Azure subscription.</span></span>

<span data-ttu-id="54fb4-125">**Ejemplo 2**</span><span class="sxs-lookup"><span data-stu-id="54fb4-125">**Example 2**</span></span>

<span data-ttu-id="54fb4-126">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="54fb4-127">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="54fb4-128">Este comando de PowerShell devuelve información acerca de todos los trabajos de análisis de transmisiones de hello en grupo de recursos de hello StreamAnalytics predeterminado-centro de EE.</span><span class="sxs-lookup"><span data-stu-id="54fb4-128">This PowerShell command returns information about all hello Stream Analytics jobs in hello resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="54fb4-129">**Ejemplo 3**</span><span class="sxs-lookup"><span data-stu-id="54fb4-129">**Example 3**</span></span>

<span data-ttu-id="54fb4-130">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="54fb4-131">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="54fb4-132">Este comando de PowerShell devuelve información sobre el trabajo de análisis de transmisiones de hello StreamingJob en grupo de recursos de hello StreamAnalytics predeterminado-centro de EE.</span><span class="sxs-lookup"><span data-stu-id="54fb4-132">This PowerShell command returns information about hello Stream Analytics job StreamingJob in hello resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="54fb4-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="54fb4-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="54fb4-134">Enumera todas las entradas de Hola que se definen en un trabajo de análisis de transmisiones especificado u obtiene información sobre una entrada específica.</span><span class="sxs-lookup"><span data-stu-id="54fb4-134">Lists all of hello inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="54fb4-135">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="54fb4-135">**Example 1**</span></span>

<span data-ttu-id="54fb4-136">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="54fb4-137">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="54fb4-138">Este comando de PowerShell devuelve información acerca de todas las entradas de hello definidos en el trabajo de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="54fb4-138">This PowerShell command returns information about all hello inputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="54fb4-139">**Ejemplo 2**</span><span class="sxs-lookup"><span data-stu-id="54fb4-139">**Example 2**</span></span>

<span data-ttu-id="54fb4-140">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="54fb4-141">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="54fb4-142">Este comando de PowerShell devuelve información acerca de la entrada de hello denominado EntryStream definido en el trabajo de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="54fb4-142">This PowerShell command returns information about hello input named EntryStream defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="54fb4-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="54fb4-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="54fb4-144">Enumera todas las salidas de Hola que se definen en un trabajo de análisis de transmisiones especificado u obtiene información sobre un resultado concreto.</span><span class="sxs-lookup"><span data-stu-id="54fb4-144">Lists all of hello outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="54fb4-145">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="54fb4-145">**Example 1**</span></span>

<span data-ttu-id="54fb4-146">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="54fb4-147">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="54fb4-148">Este comando de PowerShell devuelve información sobre definidas en el trabajo de hello StreamingJob salidas de Hola.</span><span class="sxs-lookup"><span data-stu-id="54fb4-148">This PowerShell command returns information about hello outputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="54fb4-149">**Ejemplo 2**</span><span class="sxs-lookup"><span data-stu-id="54fb4-149">**Example 2**</span></span>

<span data-ttu-id="54fb4-150">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="54fb4-151">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="54fb4-152">Este comando de PowerShell devuelve información acerca de la salida de hello denominado salida definida en el trabajo de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="54fb4-152">This PowerShell command returns information about hello output named Output defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="54fb4-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="54fb4-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="54fb4-154">Obtiene información sobre la cuota de Hola de transmisión por secuencias unidades en una región determinada.</span><span class="sxs-lookup"><span data-stu-id="54fb4-154">Gets information about hello quota of streaming units in a specified region.</span></span>

<span data-ttu-id="54fb4-155">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="54fb4-155">**Example 1**</span></span>

<span data-ttu-id="54fb4-156">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="54fb4-157">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="54fb4-158">Este comando de PowerShell devuelve información acerca de la cuota de Hola y el uso de unidades de streaming en la región de EE. UU. Central Hola.</span><span class="sxs-lookup"><span data-stu-id="54fb4-158">This PowerShell command returns information about hello quota and usage of streaming units in hello Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="54fb4-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="54fb4-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="54fb4-160">Obtiene información sobre una transformación específica definida en un trabajo de Análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="54fb4-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="54fb4-161">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="54fb4-161">**Example 1**</span></span>

<span data-ttu-id="54fb4-162">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="54fb4-163">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="54fb4-164">Este comando de PowerShell devuelve información sobre la transformación de hello denominado StreamingJob en el trabajo de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="54fb4-164">This PowerShell command returns information about hello transformation called StreamingJob in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="54fb4-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="54fb4-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="54fb4-166">Crea otra entrada en un trabajo de Análisis de transmisiones o actualiza una determinada entrada existente.</span><span class="sxs-lookup"><span data-stu-id="54fb4-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="54fb4-167">Hello nombre de entrada de hello puede especificarse en el archivo .json de Hola o en línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="54fb4-167">hello name of hello input can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="54fb4-168">Si se especifican ambos, debe Hola igual que hello en el archivo hello nombre hello en línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="54fb4-168">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="54fb4-169">Si especifica una entrada que ya existe y no se especifica hello: parámetro Force, Hola cmdlet le preguntará si o no tooreplace Hola los datos existentes.</span><span class="sxs-lookup"><span data-stu-id="54fb4-169">If you specify an input that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing input.</span></span>

<span data-ttu-id="54fb4-170">Si especifica Hola: el parámetro Force y especifique otra entrada nombre, entrada Hola se reemplazará sin confirmación.</span><span class="sxs-lookup"><span data-stu-id="54fb4-170">If you specify hello –Force parameter and specify an existing input name, hello input will be replaced without confirmation.</span></span>

<span data-ttu-id="54fb4-171">Para obtener información detallada sobre la estructura de archivos JSON de Hola y de contenido, consulte toohello [crear entrada (análisis de transmisiones de Azure)] [ msdn-rest-api-create-stream-analytics-input] sección de hello [API de REST de administración de análisis de transmisiones Biblioteca de referencia de][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="54fb4-171">For detailed information on hello JSON file structure and contents, refer toohello [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="54fb4-172">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="54fb4-172">**Example 1**</span></span>

<span data-ttu-id="54fb4-173">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="54fb4-174">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="54fb4-175">Este comando de PowerShell crea una nueva entrada de archivo hello Input.json.</span><span class="sxs-lookup"><span data-stu-id="54fb4-175">This PowerShell command creates a new input from hello file Input.json.</span></span> <span data-ttu-id="54fb4-176">Si ya hay definida una entrada existente con el nombre de hello especificado en el archivo de definición de entrada de hello, Hola cmdlet le preguntará si tooreplace se.</span><span class="sxs-lookup"><span data-stu-id="54fb4-176">If an existing input with hello name specified in hello input definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="54fb4-177">**Ejemplo 2**</span><span class="sxs-lookup"><span data-stu-id="54fb4-177">**Example 2**</span></span>

<span data-ttu-id="54fb4-178">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="54fb4-179">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="54fb4-180">Este comando de PowerShell crea una nueva entrada en el trabajo de hello denominado EntryStream.</span><span class="sxs-lookup"><span data-stu-id="54fb4-180">This PowerShell command creates a new input in hello job called EntryStream.</span></span> <span data-ttu-id="54fb4-181">Si una entrada existente con este nombre ya está definida, Hola cmdlet le preguntará si tooreplace se.</span><span class="sxs-lookup"><span data-stu-id="54fb4-181">If an existing input with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="54fb4-182">**Ejemplo 3**</span><span class="sxs-lookup"><span data-stu-id="54fb4-182">**Example 3**</span></span>

<span data-ttu-id="54fb4-183">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="54fb4-184">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="54fb4-185">Este comando de PowerShell reemplaza la definición de Hola Hola existente de origen de entrada llamado EntryStream con definición Hola desde archivo hello.</span><span class="sxs-lookup"><span data-stu-id="54fb4-185">This PowerShell command replaces hello definition of hello existing input source called EntryStream with hello definition from hello file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="54fb4-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="54fb4-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="54fb4-187">Crea un nuevo trabajo de análisis de transmisiones de Microsoft Azure o actualiza la definición de Hola de un trabajo existente especificado.</span><span class="sxs-lookup"><span data-stu-id="54fb4-187">Creates a new Stream Analytics job in Microsoft Azure, or updates hello definition of an existing specified job.</span></span>

<span data-ttu-id="54fb4-188">nombre de Hello del trabajo de hello puede especificarse en el archivo .json de Hola o en línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="54fb4-188">hello name of hello job can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="54fb4-189">Si se especifican ambos, debe Hola igual que hello en el archivo hello nombre hello en línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="54fb4-189">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="54fb4-190">Si especifica un nombre de trabajo que ya existe y no se especifica hello: parámetro Force, Hola cmdlet le preguntará si o no tooreplace Hola trabajo existente.</span><span class="sxs-lookup"><span data-stu-id="54fb4-190">If you specify a job name that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing job.</span></span>

<span data-ttu-id="54fb4-191">Si especifica Hola: el parámetro Force y especificar un nombre de trabajo existente, se reemplazará la definición del trabajo Hola sin confirmación.</span><span class="sxs-lookup"><span data-stu-id="54fb4-191">If you specify hello –Force parameter and specify an existing job name, hello job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="54fb4-192">Para obtener información detallada sobre la estructura de archivos JSON de Hola y de contenido, consulte toohello [crear trabajo de Stream Analytics] [ msdn-rest-api-create-stream-analytics-job] sección de hello [referencia de API de REST de administración de análisis de transmisiones Biblioteca][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="54fb4-192">For detailed information on hello JSON file structure and contents, refer toohello [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="54fb4-193">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="54fb4-193">**Example 1**</span></span>

<span data-ttu-id="54fb4-194">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="54fb4-195">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="54fb4-196">Este comando de PowerShell crea un nuevo trabajo de definición de hello en JobDefinition.json.</span><span class="sxs-lookup"><span data-stu-id="54fb4-196">This PowerShell command creates a new job from hello definition in JobDefinition.json.</span></span> <span data-ttu-id="54fb4-197">Si ya está definido un trabajo existente con el nombre de hello especificado en el archivo de definición de trabajo de hello, Hola cmdlet le preguntará si tooreplace se.</span><span class="sxs-lookup"><span data-stu-id="54fb4-197">If an existing job with hello name specified in hello job definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="54fb4-198">**Ejemplo 2**</span><span class="sxs-lookup"><span data-stu-id="54fb4-198">**Example 2**</span></span>

<span data-ttu-id="54fb4-199">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="54fb4-200">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="54fb4-201">Este comando de PowerShell reemplaza la definición del trabajo Hola para StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="54fb4-201">This PowerShell command replaces hello job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="54fb4-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="54fb4-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="54fb4-203">Crea una salida en un trabajo de Análisis de transmisiones o actualiza una salida existente.</span><span class="sxs-lookup"><span data-stu-id="54fb4-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="54fb4-204">nombre de Hola de salida de hello puede especificarse en el archivo .json de Hola o en línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="54fb4-204">hello name of hello output can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="54fb4-205">Si se especifican ambos, debe Hola igual que hello en el archivo hello nombre hello en línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="54fb4-205">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="54fb4-206">Si especifica una salida que ya existe y no se especifica hello: parámetro Force, Hola cmdlet le preguntará si o no tooreplace Hola salida existente.</span><span class="sxs-lookup"><span data-stu-id="54fb4-206">If you specify an output that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing output.</span></span>

<span data-ttu-id="54fb4-207">Si especifica Hola: el parámetro Force y especifique el nombre de salida de una existente, se reemplazará la salida de hello sin confirmación.</span><span class="sxs-lookup"><span data-stu-id="54fb4-207">If you specify hello –Force parameter and specify an existing output name, hello output will be replaced without confirmation.</span></span>

<span data-ttu-id="54fb4-208">Para obtener información detallada sobre la estructura de archivos JSON de Hola y de contenido, consulte toohello [crear salida (análisis de transmisiones de Azure)] [ msdn-rest-api-create-stream-analytics-output] sección de hello [API de REST de administración de análisis de transmisiones Biblioteca de referencia de][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="54fb4-208">For detailed information on hello JSON file structure and contents, refer toohello [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="54fb4-209">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="54fb4-209">**Example 1**</span></span>

<span data-ttu-id="54fb4-210">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="54fb4-211">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="54fb4-212">Este comando de PowerShell crea una nueva llamada "salida" en el trabajo de hello StreamingJob de salida.</span><span class="sxs-lookup"><span data-stu-id="54fb4-212">This PowerShell command creates a new output called "output" in hello job StreamingJob.</span></span> <span data-ttu-id="54fb4-213">Si una salida existente con este nombre ya está definida, Hola cmdlet le preguntará si tooreplace se.</span><span class="sxs-lookup"><span data-stu-id="54fb4-213">If an existing output with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="54fb4-214">**Ejemplo 2**</span><span class="sxs-lookup"><span data-stu-id="54fb4-214">**Example 2**</span></span>

<span data-ttu-id="54fb4-215">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="54fb4-216">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="54fb4-217">Este comando de PowerShell reemplaza la definición de Hola de "salida" en el trabajo de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="54fb4-217">This PowerShell command replaces hello definition for "output" in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="54fb4-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="54fb4-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="54fb4-219">Crea una nueva transformación dentro de un trabajo de análisis de transmisiones o actualiza transformación existente Hola.</span><span class="sxs-lookup"><span data-stu-id="54fb4-219">Creates a new transformation within a Stream Analytics job, or updates hello existing transformation.</span></span>

<span data-ttu-id="54fb4-220">nombre de Hola de transformación de Hola puede especificarse en el archivo .json de Hola o en línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="54fb4-220">hello name of hello transformation can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="54fb4-221">Si se especifican ambos, debe Hola igual que hello en el archivo hello nombre hello en línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="54fb4-221">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="54fb4-222">Si especifica una transformación que ya existe y no se especifica hello: parámetro Force, Hola cmdlet le preguntará si o no tooreplace Hola transformación existente.</span><span class="sxs-lookup"><span data-stu-id="54fb4-222">If you specify a transformation that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing transformation.</span></span>

<span data-ttu-id="54fb4-223">Si especifica Hola: el parámetro Force y especificar un nombre de la transformación existente, se reemplazará la transformación de hello sin confirmación.</span><span class="sxs-lookup"><span data-stu-id="54fb4-223">If you specify hello –Force parameter and specify an existing transformation name, hello transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="54fb4-224">Para obtener información detallada sobre la estructura de archivos JSON de Hola y de contenido, consulte toohello [crear una transformación (análisis de transmisiones de Azure)] [ msdn-rest-api-create-stream-analytics-transformation] sección de hello [administración de análisis de transmisiones Biblioteca de referencia de API de REST][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="54fb4-224">For detailed information on hello JSON file structure and contents, refer toohello [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="54fb4-225">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="54fb4-225">**Example 1**</span></span>

<span data-ttu-id="54fb4-226">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="54fb4-227">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="54fb4-228">Este comando de PowerShell crea una nueva transformación denominada StreamingJobTransform en el trabajo de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="54fb4-228">This PowerShell command creates a new transformation called StreamingJobTransform in hello job StreamingJob.</span></span> <span data-ttu-id="54fb4-229">Si una transformación existente ya está definida con este nombre, Hola cmdlet le preguntará si tooreplace se.</span><span class="sxs-lookup"><span data-stu-id="54fb4-229">If an existing transformation is already defined with this name, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="54fb4-230">**Ejemplo 2**</span><span class="sxs-lookup"><span data-stu-id="54fb4-230">**Example 2**</span></span>

<span data-ttu-id="54fb4-231">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="54fb4-232">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="54fb4-233">Este comando de PowerShell reemplaza la definición de Hola de StreamingJobTransform en el trabajo de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="54fb4-233">This PowerShell command replaces hello definition of StreamingJobTransform in hello job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="54fb4-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="54fb4-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="54fb4-235">Elimina de forma asincrónica una entrada específica desde un trabajo de Análisis de transmisiones en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="54fb4-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="54fb4-236">Si especifica hello: parámetro Force, Hola de entrada se eliminará sin confirmación.</span><span class="sxs-lookup"><span data-stu-id="54fb4-236">If you specify hello –Force parameter, hello input will be deleted without confirmation.</span></span>

<span data-ttu-id="54fb4-237">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="54fb4-237">**Example 1**</span></span>

<span data-ttu-id="54fb4-238">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="54fb4-239">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="54fb4-240">Este comando de PowerShell quita Hola EventStream de entrada en el trabajo de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="54fb4-240">This PowerShell command removes hello input EventStream in hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="54fb4-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="54fb4-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="54fb4-242">Elimina de forma asincrónica un trabajo específico de Análisis de transmisiones en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="54fb4-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="54fb4-243">Si especifica hello: parámetro Force, Hola trabajo será eliminado sin confirmación.</span><span class="sxs-lookup"><span data-stu-id="54fb4-243">If you specify hello –Force parameter, hello job will be deleted without confirmation.</span></span>

<span data-ttu-id="54fb4-244">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="54fb4-244">**Example 1**</span></span>

<span data-ttu-id="54fb4-245">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="54fb4-246">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="54fb4-247">Este comando de PowerShell quita el trabajo de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="54fb4-247">This PowerShell command removes hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="54fb4-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="54fb4-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="54fb4-249">Elimina de forma asincrónica un resultado concreto de un trabajo de Análisis de transmisiones en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="54fb4-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="54fb4-250">Si especifica hello: parámetro Force, Hola resultado será eliminado sin confirmación.</span><span class="sxs-lookup"><span data-stu-id="54fb4-250">If you specify hello –Force parameter, hello output will be deleted without confirmation.</span></span>

<span data-ttu-id="54fb4-251">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="54fb4-251">**Example 1**</span></span>

<span data-ttu-id="54fb4-252">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="54fb4-253">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="54fb4-254">Este comando de PowerShell quita hello salida salida en el trabajo de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="54fb4-254">This PowerShell command removes hello output Output in hello job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="54fb4-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="54fb4-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="54fb4-256">Implementa e inicia un trabajo de Análisis de transmisiones de Microsoft Azure de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="54fb4-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="54fb4-257">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="54fb4-257">**Example 1**</span></span>

<span data-ttu-id="54fb4-258">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="54fb4-259">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="54fb4-260">Este comando de PowerShell inicia Hola trabajo StreamingJob con una hora de inicio de salida personalizada establece tooDecember 12, 2012, 12:12:12 UTC.</span><span class="sxs-lookup"><span data-stu-id="54fb4-260">This PowerShell command starts hello job StreamingJob with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="54fb4-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="54fb4-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="54fb4-262">Detiene la ejecución de un trabajo de Análisis de transmisiones en Microsoft Azure y desasigna recursos que se usaban de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="54fb4-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="54fb4-263">Hello metadatos y la definición de trabajo seguirán estando disponibles dentro de su suscripción a través de hello portal de Azure y API de administración, por ejemplo, que hello trabajo puede editar y reiniciar.</span><span class="sxs-lookup"><span data-stu-id="54fb4-263">hello job definition and metadata will remain available within your subscription through both hello Azure portal and management APIs, such that hello job can be edited and restarted.</span></span> <span data-ttu-id="54fb4-264">No se le cobrará por un trabajo en el estado de hello detenido.</span><span class="sxs-lookup"><span data-stu-id="54fb4-264">You will not be charged for a job in hello stopped state.</span></span>

<span data-ttu-id="54fb4-265">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="54fb4-265">**Example 1**</span></span>

<span data-ttu-id="54fb4-266">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="54fb4-267">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="54fb4-268">Este comando de PowerShell detiene el trabajo de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="54fb4-268">This PowerShell command stops hello job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="54fb4-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="54fb4-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="54fb4-270">Posibilidad de Hola de pruebas de análisis de transmisiones tooconnect tooa especifica la entrada.</span><span class="sxs-lookup"><span data-stu-id="54fb4-270">Tests hello ability of Stream Analytics tooconnect tooa specified input.</span></span>

<span data-ttu-id="54fb4-271">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="54fb4-271">**Example 1**</span></span>

<span data-ttu-id="54fb4-272">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="54fb4-273">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="54fb4-274">Este estado de conexión de PowerShell comando pruebas Hola de hello EntryStream en StreamingJob de entrada.</span><span class="sxs-lookup"><span data-stu-id="54fb4-274">This PowerShell command tests hello connection status of hello input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="54fb4-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="54fb4-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="54fb4-276">Posibilidad de Hola de pruebas de análisis de transmisiones tooconnect tooa especifica la salida.</span><span class="sxs-lookup"><span data-stu-id="54fb4-276">Tests hello ability of Stream Analytics tooconnect tooa specified output.</span></span>

<span data-ttu-id="54fb4-277">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="54fb4-277">**Example 1**</span></span>

<span data-ttu-id="54fb4-278">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="54fb4-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="54fb4-279">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="54fb4-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="54fb4-280">Este estado de conexión de PowerShell comando pruebas Hola de hello salida salida en StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="54fb4-280">This PowerShell command tests hello connection status of hello output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="54fb4-281">Obtención de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="54fb4-281">Get support</span></span>
<span data-ttu-id="54fb4-282">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="54fb4-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="54fb4-283">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="54fb4-283">Next steps</span></span>
* [<span data-ttu-id="54fb4-284">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="54fb4-284">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="54fb4-285">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="54fb4-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="54fb4-286">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="54fb4-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="54fb4-287">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="54fb4-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="54fb4-288">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="54fb4-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

