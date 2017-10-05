---
title: "Supervisión de Azure Functions | Microsoft Docs"
description: Aprenda a supervisar Azure Functions.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "Azure funciones, funciones, procesamiento de eventos, webhooks, proceso dinámico, arquitectura sin servidor"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: b70214593b1417265387f42306a633bb0df2920e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="51ac4-104">Supervisión de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="51ac4-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="51ac4-105">Información general</span><span class="sxs-lookup"><span data-stu-id="51ac4-105">Overview</span></span> 


<span data-ttu-id="51ac4-106">La pestaña **Monitor** (Supervisar) en cada función le permite revisar cada ejecución de una función.</span><span class="sxs-lookup"><span data-stu-id="51ac4-106">The **Monitor** tab for each function allows you to review each execution of a function.</span></span>

![Pestaña de supervisión de Azure Functions](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="51ac4-108">Al hacer clic en una ejecución puede revisar la duración, los datos de entrada, los errores y los archivos de registro asociados.</span><span class="sxs-lookup"><span data-stu-id="51ac4-108">Clicking an execution allows you to review the duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="51ac4-109">Esto resulta de utilidad con vistas a la depuración y la optimización del rendimiento de sus funciones.</span><span class="sxs-lookup"><span data-stu-id="51ac4-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="51ac4-110">Al usar el [plan de hospedaje de consumo](functions-overview.md#pricing) para Azure Functions, el icono **Monitoring** (Supervisión) de la hoja de información general de Function App no muestra ningún dato.</span><span class="sxs-lookup"><span data-stu-id="51ac4-110">When using the [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, the **Monitoring** tile in the Function App overview blade will not show any data.</span></span> <span data-ttu-id="51ac4-111">Esto se debe a que la plataforma escala y administra las instancias de proceso de manera dinámica sin intervención del usuario, por lo que estas métricas no son significativas en un plan de consumo.</span><span class="sxs-lookup"><span data-stu-id="51ac4-111">This is because the platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="51ac4-112">Para supervisar el uso de las aplicaciones de función, debe guiarse por los pasos que se indican en este artículo.</span><span class="sxs-lookup"><span data-stu-id="51ac4-112">To monitor the usage of your Function Apps, you should instead use the guidance in this article.</span></span>
> 
> <span data-ttu-id="51ac4-113">La siguiente captura de pantalla muestra un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="51ac4-113">The following screen-shot shows an example:</span></span>
> 
> ![Hoja de supervisión del recurso principal](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="51ac4-115">Supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="51ac4-115">Real-time monitoring</span></span>

<span data-ttu-id="51ac4-116">La supervisión en tiempo real está disponible cuando se hace clic en **secuencia de eventos en directo**, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="51ac4-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Opción de secuencia de eventos en directo de la pestaña de supervisión](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="51ac4-118">La secuencia de eventos en directo se representa gráficamente en una nueva pestaña de explorador, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="51ac4-118">The live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Ejemplo de secuencia de eventos en directo](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="51ac4-120">Existe un problema conocido que puede provocar que no se pueden rellenar los datos.</span><span class="sxs-lookup"><span data-stu-id="51ac4-120">There is a known issue that may cause your data to fail to be populated.</span></span> <span data-ttu-id="51ac4-121">Si experimenta este problema, puede que tenga que cerrar la pestaña del explorador que contiene la secuencia de eventos en directo y luego hacer clic de nuevo en **secuencia de eventos en directo** para poder rellenar correctamente los datos de la secuencia de eventos.</span><span class="sxs-lookup"><span data-stu-id="51ac4-121">If you experience this, you may need to close the browser tab containing the live event stream and then click **live event stream** again to allow it to properly populate your event stream data.</span></span> 

<span data-ttu-id="51ac4-122">La secuencia de eventos en directo representará gráficamente las siguientes estadísticas de su función:</span><span class="sxs-lookup"><span data-stu-id="51ac4-122">The live event stream will graph the following statistics for your function:</span></span>

* <span data-ttu-id="51ac4-123">Ejecuciones iniciadas por segundo</span><span class="sxs-lookup"><span data-stu-id="51ac4-123">Executions started per second</span></span>
* <span data-ttu-id="51ac4-124">Ejecuciones finalizadas por segundo</span><span class="sxs-lookup"><span data-stu-id="51ac4-124">Executions completed per second</span></span>
* <span data-ttu-id="51ac4-125">Ejecuciones con error por segundo</span><span class="sxs-lookup"><span data-stu-id="51ac4-125">Executions failed per second</span></span>
* <span data-ttu-id="51ac4-126">Tiempo medio de ejecución en milisegundos</span><span class="sxs-lookup"><span data-stu-id="51ac4-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="51ac4-127">Estas estadísticas son en tiempo real, pero el gráfico real de los datos de ejecución puede tener alrededor de 10 segundos de latencia.</span><span class="sxs-lookup"><span data-stu-id="51ac4-127">These statistics are real-time but the actual graphing of the execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="51ac4-128">Supervisión de archivos de registro desde una línea de comandos</span><span class="sxs-lookup"><span data-stu-id="51ac4-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="51ac4-129">Puede transmitir archivos de registro a una sesión de línea de comandos en una estación de trabajo local mediante la interfaz de la línea de comandos (CLI) de Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="51ac4-129">You can stream log files to a command line session on a local workstation using the Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-the-azure-cli"></a><span data-ttu-id="51ac4-130">Supervisión de archivos de registro de aplicación de función con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="51ac4-130">Monitoring function app log files with the Azure CLI</span></span>

<span data-ttu-id="51ac4-131">Para comenzar, [instale la CLI de Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="51ac4-131">To get started, [install the Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="51ac4-132">Inicie sesión en su cuenta de Azure mediante el siguiente comando, o cualquiera de las otras opciones que se tratan en [Inicio de sesión en Azure desde la CLI de Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="51ac4-132">Log into your Azure account using the following command, or any of the other options covered in, [Log in to Azure from the Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="51ac4-133">Use el siguiente comando para habilitar el modo de administración de servicios de la CLI de Azure (ASM).</span><span class="sxs-lookup"><span data-stu-id="51ac4-133">Use the following command to enable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="51ac4-134">Si tiene varias suscripciones, use los siguientes comandos para mostrar las suscripciones y establecer la suscripción actual como la suscripción que contiene la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="51ac4-134">If you have multiple subscriptions, use the following commands to list your subscriptions and set the current subscription to the subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="51ac4-135">El siguiente comando transmitirá los archivos de registro de la aplicación de función a la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="51ac4-135">The following command will stream the log files of your function app to the command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="51ac4-136">Supervisión de archivos de registro de aplicación de función con PowerShell</span><span class="sxs-lookup"><span data-stu-id="51ac4-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="51ac4-137">Para comenzar, [instale y configure Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="51ac4-137">To get started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="51ac4-138">Agregue la cuenta de Azure; para ello, haga clic en el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="51ac4-138">Add your Azure account by running the following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="51ac4-139">Si tiene varias suscripciones, puede mostrarlas por nombre con el siguiente comando para ver si la suscripción correcta es la seleccionada actualmente según la propiedad `IsCurrent`:</span><span class="sxs-lookup"><span data-stu-id="51ac4-139">If you have multiple subscriptions, you can list them by name with the following command to see if the correct subscription is the currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="51ac4-140">Si necesita que la suscripción activa sea la que contiene la aplicación de función, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="51ac4-140">If you need to set the active subscription to the one containing your function app, use the following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="51ac4-141">Transmita los registros a la sesión de PowerShell con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="51ac4-141">Stream the logs to your PowerShell session with the following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="51ac4-142">Para más información, consulte [Transmisión de registros para aplicaciones web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="51ac4-142">For more information refer to [How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="51ac4-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="51ac4-143">Next steps</span></span>
<span data-ttu-id="51ac4-144">Para obtener más información, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="51ac4-144">For more information, see the following resources:</span></span>

* [<span data-ttu-id="51ac4-145">Prueba de una función</span><span class="sxs-lookup"><span data-stu-id="51ac4-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="51ac4-146">Escalar una función</span><span class="sxs-lookup"><span data-stu-id="51ac4-146">Scale a function</span></span>](functions-scale.md)

