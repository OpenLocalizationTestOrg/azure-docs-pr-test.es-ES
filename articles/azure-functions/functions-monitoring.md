---
title: aaaMonitoring funciones de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomonitor las funciones de Azure."
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
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="6f8c7-104">Supervisión de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="6f8c7-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="6f8c7-105">Información general</span><span class="sxs-lookup"><span data-stu-id="6f8c7-105">Overview</span></span> 


<span data-ttu-id="6f8c7-106">Hola **Monitor** pestaña para cada función le permite tooreview cada ejecución de una función.</span><span class="sxs-lookup"><span data-stu-id="6f8c7-106">hello **Monitor** tab for each function allows you tooreview each execution of a function.</span></span>

![Pestaña de supervisión de Azure Functions](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="6f8c7-108">Al hacer clic en una ejecución permite duración hello tooreview, datos de entrada, errores y archivos de registro asociados.</span><span class="sxs-lookup"><span data-stu-id="6f8c7-108">Clicking an execution allows you tooreview hello duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="6f8c7-109">Esto resulta de utilidad con vistas a la depuración y la optimización del rendimiento de sus funciones.</span><span class="sxs-lookup"><span data-stu-id="6f8c7-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="6f8c7-110">Cuando se usa hello [consumo de plan de hospedaje](functions-overview.md#pricing) para las funciones de Azure, Hola **supervisión** icono en hoja de información general sobre la aplicación de la función hello no mostrará ningún dato.</span><span class="sxs-lookup"><span data-stu-id="6f8c7-110">When using hello [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, hello **Monitoring** tile in hello Function App overview blade will not show any data.</span></span> <span data-ttu-id="6f8c7-111">Esto es porque la plataforma de hello dinámicamente escala y administra las instancias de proceso en su nombre, por lo que estas métricas no son significativas en un plan de consumo.</span><span class="sxs-lookup"><span data-stu-id="6f8c7-111">This is because hello platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="6f8c7-112">uso de hello toomonitor de las aplicaciones de la función, en su lugar, debe utilizar las directrices de hello en este artículo.</span><span class="sxs-lookup"><span data-stu-id="6f8c7-112">toomonitor hello usage of your Function Apps, you should instead use hello guidance in this article.</span></span>
> 
> <span data-ttu-id="6f8c7-113">Hola siguiente captura de pantalla muestra un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6f8c7-113">hello following screen-shot shows an example:</span></span>
> 
> ![Supervisión en la hoja de recursos principal Hola](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="6f8c7-115">Supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="6f8c7-115">Real-time monitoring</span></span>

<span data-ttu-id="6f8c7-116">La supervisión en tiempo real está disponible cuando se hace clic en **secuencia de eventos en directo**, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="6f8c7-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Opción de secuencia de eventos de la pestaña monitor de Hola de vida](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="6f8c7-118">secuencia de eventos en directo de Hola se representa gráficamente en una nueva pestaña de explorador tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="6f8c7-118">hello live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Ejemplo de secuencia de eventos en directo](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="6f8c7-120">Hay un problema conocido que puede provocar la toobe de toofail de datos rellena.</span><span class="sxs-lookup"><span data-stu-id="6f8c7-120">There is a known issue that may cause your data toofail toobe populated.</span></span> <span data-ttu-id="6f8c7-121">Si sucede esto, puede que tenga tooclose Hola explorador pestaña contenedor Hola eventos en vivo secuencia y, a continuación, haga clic en **flujo de eventos en vivo** nuevo tooallow se tooproperly rellenar los datos de la secuencia de eventos.</span><span class="sxs-lookup"><span data-stu-id="6f8c7-121">If you experience this, you may need tooclose hello browser tab containing hello live event stream and then click **live event stream** again tooallow it tooproperly populate your event stream data.</span></span> 

<span data-ttu-id="6f8c7-122">secuencia de eventos en directo de Hola graph Hola siguiendo las estadísticas de la función:</span><span class="sxs-lookup"><span data-stu-id="6f8c7-122">hello live event stream will graph hello following statistics for your function:</span></span>

* <span data-ttu-id="6f8c7-123">Ejecuciones iniciadas por segundo</span><span class="sxs-lookup"><span data-stu-id="6f8c7-123">Executions started per second</span></span>
* <span data-ttu-id="6f8c7-124">Ejecuciones finalizadas por segundo</span><span class="sxs-lookup"><span data-stu-id="6f8c7-124">Executions completed per second</span></span>
* <span data-ttu-id="6f8c7-125">Ejecuciones con error por segundo</span><span class="sxs-lookup"><span data-stu-id="6f8c7-125">Executions failed per second</span></span>
* <span data-ttu-id="6f8c7-126">Tiempo medio de ejecución en milisegundos</span><span class="sxs-lookup"><span data-stu-id="6f8c7-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="6f8c7-127">Estas estadísticas son en tiempo real pero Hola real generar gráficos de datos de ejecución de hello puede tener unos 10 segundos de latencia.</span><span class="sxs-lookup"><span data-stu-id="6f8c7-127">These statistics are real-time but hello actual graphing of hello execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="6f8c7-128">Supervisión de archivos de registro desde una línea de comandos</span><span class="sxs-lookup"><span data-stu-id="6f8c7-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="6f8c7-129">Puede transmitir la sesión de línea de comandos de tooa de archivos de registro en una estación de trabajo local mediante Hola interfaz de línea de comandos (CLI) de Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f8c7-129">You can stream log files tooa command line session on a local workstation using hello Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a><span data-ttu-id="6f8c7-130">Supervisión de archivos de registro de aplicación de función con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="6f8c7-130">Monitoring function app log files with hello Azure CLI</span></span>

<span data-ttu-id="6f8c7-131">tooget iniciado, [instalar Hola CLI de Azure](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="6f8c7-131">tooget started, [install hello Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="6f8c7-132">Inicie sesión en su cuenta de Azure con hello siguientes comando, o cualquiera de Hola otras opciones que se abordan en, [sesión tooAzure de hello Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="6f8c7-132">Log into your Azure account using hello following command, or any of hello other options covered in, [Log in tooAzure from hello Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="6f8c7-133">Siguiente Hola de uso del comando tooenable el modo de administración de servicio de CLI de Azure (ASM):.</span><span class="sxs-lookup"><span data-stu-id="6f8c7-133">Use hello following command tooenable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="6f8c7-134">Si tiene varias suscripciones, use Hola después a toolist de comandos las suscripciones y el conjunto de hello suscripción toohello suscripción actual que contiene la aplicación de la función.</span><span class="sxs-lookup"><span data-stu-id="6f8c7-134">If you have multiple subscriptions, use hello following commands toolist your subscriptions and set hello current subscription toohello subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="6f8c7-135">Hello siguiente comando transmiten los archivos de registro de hello de la línea de comandos de toohello de aplicación de función:</span><span class="sxs-lookup"><span data-stu-id="6f8c7-135">hello following command will stream hello log files of your function app toohello command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="6f8c7-136">Supervisión de archivos de registro de aplicación de función con PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f8c7-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="6f8c7-137">tooget iniciado, [instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6f8c7-137">tooget started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="6f8c7-138">Agregue su cuenta de Azure ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="6f8c7-138">Add your Azure account by running hello following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="6f8c7-139">Si tiene varias suscripciones, pueden mostrarse por nombre con hello después toosee comando si Hola correcto de suscripción es hello actualmente seleccionado se basa en `IsCurrent` propiedad:</span><span class="sxs-lookup"><span data-stu-id="6f8c7-139">If you have multiple subscriptions, you can list them by name with hello following command toosee if hello correct subscription is hello currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="6f8c7-140">Si necesita tooset Hola suscripción activa toohello uno que contenga la aplicación de la función, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="6f8c7-140">If you need tooset hello active subscription toohello one containing your function app, use hello following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="6f8c7-141">Sesión de PowerShell tooyour y registros de hello secuencia con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="6f8c7-141">Stream hello logs tooyour PowerShell session with hello following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="6f8c7-142">Para obtener más información, consulte demasiado[Cómo: transmitir por secuencias registros para las aplicaciones web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="6f8c7-142">For more information refer too[How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6f8c7-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6f8c7-143">Next steps</span></span>
<span data-ttu-id="6f8c7-144">Para obtener más información, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6f8c7-144">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="6f8c7-145">Prueba de una función</span><span class="sxs-lookup"><span data-stu-id="6f8c7-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="6f8c7-146">Escalar una función</span><span class="sxs-lookup"><span data-stu-id="6f8c7-146">Scale a function</span></span>](functions-scale.md)

