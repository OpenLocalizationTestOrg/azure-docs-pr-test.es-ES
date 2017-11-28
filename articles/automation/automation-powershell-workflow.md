---
title: "aaaLearning flujo de trabajo de PowerShell para la automatización de Azure | Documentos de Microsoft"
description: "Este artículo está pensado como una lección rápida para los autores familiarizados con PowerShell toounderstand hello las diferencias específicas entre PowerShell y flujo de trabajo de PowerShell y runbooks de conceptos tooAutomation aplicables."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 84bf133e-5343-4e0e-8d6c-bb14304a70db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 362c504eb96d31b99a826b128e6a591beecaa084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="828a7-103">Aprendizaje de los conceptos básicos del flujo de trabajo de Windows PowerShell para los runbooks de Automation</span><span class="sxs-lookup"><span data-stu-id="828a7-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="828a7-104">Los runbooks de Azure Automation se implementan como flujos de trabajo de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="828a7-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="828a7-105">Un flujo de trabajo de Windows PowerShell es el script de Windows PowerShell tooa similar pero presenta algunas diferencias importantes que pueden ser confusos tooa nuevo usuario.</span><span class="sxs-lookup"><span data-stu-id="828a7-105">A Windows PowerShell Workflow is similar tooa Windows PowerShell script but has some significant differences that can be confusing tooa new user.</span></span>  <span data-ttu-id="828a7-106">Aunque este artículo está previsto toohelp escribir runbooks mediante el flujo de trabajo de PowerShell, se recomienda que escribir runbooks con PowerShell, a menos que tenga puntos de control.</span><span class="sxs-lookup"><span data-stu-id="828a7-106">While this article is intended toohelp you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="828a7-107">Hay varias diferencias de sintaxis al crear runbooks de flujo de trabajo de PowerShell y estas diferencias requieren un poco más trabajo toowrite efectivo los flujos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="828a7-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work toowrite effective workflows.</span></span>  

<span data-ttu-id="828a7-108">Un flujo de trabajo es una secuencia de pasos conectados y programados que realizan tareas de larga duración o requieren la coordinación de Hola de varios pasos en varios dispositivos o nodos administrados.</span><span class="sxs-lookup"><span data-stu-id="828a7-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require hello coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="828a7-109">ventajas de un flujo de trabajo en un script normal Hello incluyen capacidad de hello toosimultaneously realizar una acción en varios dispositivos y Hola capacidad tooautomatically recuperarse de errores.</span><span class="sxs-lookup"><span data-stu-id="828a7-109">hello benefits of a workflow over a normal script include hello ability toosimultaneously perform an action against multiple devices and hello ability tooautomatically recover from failures.</span></span> <span data-ttu-id="828a7-110">Un flujo de trabajo de Windows PowerShell es un script de Windows PowerShell que usa Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="828a7-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="828a7-111">Mientras el flujo de trabajo de Hola se escribe con sintaxis de Windows PowerShell y se inicia mediante Windows PowerShell, se procesa mediante Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="828a7-111">While hello workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="828a7-112">Para obtener información detallada sobre los temas de hello en este artículo, consulte [Introducción a Workflow de Windows PowerShell](http://technet.microsoft.com/library/jj134242.aspx).</span><span class="sxs-lookup"><span data-stu-id="828a7-112">For complete details on hello topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="828a7-113">Estructura básica de un flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="828a7-113">Basic structure of a workflow</span></span>
<span data-ttu-id="828a7-114">Hello primer paso tooconverting un flujo de trabajo de PowerShell de PowerShell script tooa incluye con hello **flujo de trabajo** palabra clave.</span><span class="sxs-lookup"><span data-stu-id="828a7-114">hello first step tooconverting a PowerShell script tooa PowerShell workflow is enclosing it with hello **Workflow** keyword.</span></span>  <span data-ttu-id="828a7-115">Inicia un flujo de trabajo con hello **flujo de trabajo** palabra clave seguida de cuerpo de Hola de script de Hola encerrado entre llaves.</span><span class="sxs-lookup"><span data-stu-id="828a7-115">A workflow starts with hello **Workflow** keyword followed by hello body of hello script enclosed in braces.</span></span> <span data-ttu-id="828a7-116">nombre de Hola de flujo de trabajo de hello sigue hello **flujo de trabajo** palabra clave tal y como se muestra en hello según la sintaxis:</span><span class="sxs-lookup"><span data-stu-id="828a7-116">hello name of hello workflow follows hello **Workflow** keyword as shown in hello following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="828a7-117">Hola nombre de flujo de trabajo de hello debe coincidir con hello de runbook de automatización de Hola.</span><span class="sxs-lookup"><span data-stu-id="828a7-117">hello name of hello workflow must match hello name of hello Automation runbook.</span></span> <span data-ttu-id="828a7-118">Si se va a importar runbook hello, Hola filename debe coincidir con el nombre de flujo de trabajo de Hola y debe terminar en *. ps1*.</span><span class="sxs-lookup"><span data-stu-id="828a7-118">If hello runbook is being imported, then hello filename must match hello workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="828a7-119">flujo de trabajo de tooadd parámetros toohello, use hello **Param** palabra clave como lo haría con script tooa.</span><span class="sxs-lookup"><span data-stu-id="828a7-119">tooadd parameters toohello workflow, use hello **Param** keyword just as you would tooa script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="828a7-120">Cambios de código</span><span class="sxs-lookup"><span data-stu-id="828a7-120">Code changes</span></span>
<span data-ttu-id="828a7-121">Código de flujo de trabajo de PowerShell examina el código de script de tooPowerShell casi idéntico salvo algunos cambios importantes.</span><span class="sxs-lookup"><span data-stu-id="828a7-121">PowerShell workflow code looks almost identical tooPowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="828a7-122">Hola siguientes secciones describe los cambios que necesite toomake tooa PowerShell script para toorun en un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="828a7-122">hello following sections describe changes that you need toomake tooa PowerShell script for it toorun in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="828a7-123">Actividades</span><span class="sxs-lookup"><span data-stu-id="828a7-123">Activities</span></span>
<span data-ttu-id="828a7-124">Una actividad es una tarea específica de un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="828a7-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="828a7-125">Al igual que un script se compone de uno o varios comandos, un flujo de trabajo se compone de una o varias actividades que se realizan en secuencia.</span><span class="sxs-lookup"><span data-stu-id="828a7-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="828a7-126">Flujo de trabajo de Windows PowerShell convierte automáticamente muchos de hello tooactivities de cmdlets de Windows PowerShell cuando se ejecuta un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="828a7-126">Windows PowerShell Workflow automatically converts many of hello Windows PowerShell cmdlets tooactivities when it runs a workflow.</span></span> <span data-ttu-id="828a7-127">Cuando se especifica uno de estos cmdlets en su runbook, actividad de hello correspondiente se ejecuta mediante Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="828a7-127">When you specify one of these cmdlets in your runbook, hello corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="828a7-128">Para los cmdlets sin una actividad correspondiente, el flujo de trabajo de Windows PowerShell ejecuta automáticamente Hola cmdlet dentro de un [InlineScript](#inlinescript) actividad.</span><span class="sxs-lookup"><span data-stu-id="828a7-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs hello cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="828a7-129">Hay un conjunto de cmdlets que están excluidos y no se pueden usar en un flujo de trabajo a menos que incluya explícitamente en un bloque de InlineScript.</span><span class="sxs-lookup"><span data-stu-id="828a7-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="828a7-130">Para obtener más información sobre estos conceptos, consulte [Uso de actividades en los flujos de trabajo de scripts](http://technet.microsoft.com/library/jj574194.aspx).</span><span class="sxs-lookup"><span data-stu-id="828a7-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="828a7-131">Las actividades de flujo de trabajo comparten un conjunto de tooconfigure de parámetros comunes su funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="828a7-131">Workflow activities share a set of common parameters tooconfigure their operation.</span></span> <span data-ttu-id="828a7-132">Para obtener más información acerca de los parámetros comunes de flujo de trabajo de hello, consulte [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="828a7-132">For details about hello workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="828a7-133">Parámetros posicionales</span><span class="sxs-lookup"><span data-stu-id="828a7-133">Positional parameters</span></span>
<span data-ttu-id="828a7-134">No puede usar parámetros posicionales con actividades y cmdlets en un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="828a7-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="828a7-135">Todo esto significa que debe usar nombres de parámetros.</span><span class="sxs-lookup"><span data-stu-id="828a7-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="828a7-136">Por ejemplo, considere la posibilidad de hello después el código que obtiene todos los servicios en ejecución.</span><span class="sxs-lookup"><span data-stu-id="828a7-136">For example, consider hello following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="828a7-137">Si intentas toorun este mismo código en un flujo de trabajo, recibirá un mensaje como "Parámetro de conjunto no se puede resolver con hello especificado denominado parámetros".</span><span class="sxs-lookup"><span data-stu-id="828a7-137">If you try toorun this same code in a workflow, you receive a message like "Parameter set cannot be resolved using hello specified named parameters."</span></span>  <span data-ttu-id="828a7-138">toocorrect, proporcionar nombre del parámetro hello como en el siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="828a7-138">toocorrect this, provide hello parameter name as in hello following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="828a7-139">Objetos deserializados</span><span class="sxs-lookup"><span data-stu-id="828a7-139">Deserialized objects</span></span>
<span data-ttu-id="828a7-140">Los objetos de los flujos de trabajo están deserializados.</span><span class="sxs-lookup"><span data-stu-id="828a7-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="828a7-141">Esto significa que sus propiedades siguen estando disponibles, pero no sus métodos.</span><span class="sxs-lookup"><span data-stu-id="828a7-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="828a7-142">Por ejemplo, considere la posibilidad de hello siguiente código de PowerShell que se detiene un servicio mediante el método de Stop Hola Hola de objeto de servicio.</span><span class="sxs-lookup"><span data-stu-id="828a7-142">For example, consider hello following PowerShell code that stops a service using hello Stop method of hello Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="828a7-143">Si intentas toorun esto en un flujo de trabajo, recibirá un error que indica que "no es posible invocar métodos en un flujo de trabajo de Windows PowerShell."</span><span class="sxs-lookup"><span data-stu-id="828a7-143">If you try toorun this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="828a7-144">Una opción es toowrap estas dos líneas de código en un [InlineScript](#inlinescript) bloquear en cuyo caso $Service sería un objeto de servicio dentro de bloques de Hola.</span><span class="sxs-lookup"><span data-stu-id="828a7-144">One option is toowrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within hello block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="828a7-145">Otra opción es toouse Hola a otro cmdlet que realiza la misma funcionalidad que el método de hello, si está disponible.</span><span class="sxs-lookup"><span data-stu-id="828a7-145">Another option is toouse another cmdlet that performs hello same functionality as hello method, if one is available.</span></span>  <span data-ttu-id="828a7-146">En nuestro ejemplo, el cmdlet de hello Stop-Service proporciona Hola misma funcionalidad que el método de detención de hello y podría utilizar siguiente Hola para un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="828a7-146">In our sample, hello Stop-Service cmdlet provides hello same functionality as hello Stop method, and you could use hello following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="828a7-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="828a7-147">InlineScript</span></span>
<span data-ttu-id="828a7-148">Hola **InlineScript** actividad es útil cuando necesita uno o más comandos de toorun como tradicional script de PowerShell en lugar de flujo de trabajo de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="828a7-148">hello **InlineScript** activity is useful when you need toorun one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="828a7-149">Mientras que los comandos en un flujo de trabajo se envían tooWindows Workflow Foundation para su procesamiento, comandos de un bloque de InlineScript se procesan mediante Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="828a7-149">While commands in a workflow are sent tooWindows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="828a7-150">InlineScript usa Hola sintaxis que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="828a7-150">InlineScript uses hello following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="828a7-151">Puede devolver resultados desde un InlineScript mediante la asignación de variable de tooa de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="828a7-151">You can return output from an InlineScript by assigning hello output tooa variable.</span></span> <span data-ttu-id="828a7-152">Hello en el ejemplo siguiente se detiene un servicio y, a continuación, genera el nombre del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="828a7-152">hello following example stops a service and then outputs hello service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="828a7-153">Puede pasar valores en un bloque de InlineScript, pero debe usar el modificador de ámbito **$Using** .</span><span class="sxs-lookup"><span data-stu-id="828a7-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="828a7-154">Hello en el ejemplo siguiente se es idéntico toohello ejemplo anterior salvo que hello nombre de servicio proporciona una variable.</span><span class="sxs-lookup"><span data-stu-id="828a7-154">hello following example is identical toohello previous example except that hello service name is provided by a variable.</span></span>

    Workflow Stop-MyService
    {
        $ServiceName = "MyService"

        $Output = InlineScript {
            $Service = Get-Service -Name $Using:ServiceName
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="828a7-155">Aunque las actividades de InlineScript pueden resultar fundamental en ciertos flujos de trabajo, no se son compatibles con construcciones de flujo de trabajo y sólo debe utilizarse cuando sea necesario para hello siguientes motivos:</span><span class="sxs-lookup"><span data-stu-id="828a7-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for hello following reasons:</span></span>

* <span data-ttu-id="828a7-156">No puede usar [puntos de comprobación](#checkpoints) dentro de un bloque de InlineScript.</span><span class="sxs-lookup"><span data-stu-id="828a7-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="828a7-157">Si se produce un error en el bloque de hello, se debe reanudar desde principio Hola del bloque de Hola.</span><span class="sxs-lookup"><span data-stu-id="828a7-157">If a failure occurs within hello block, it must be resumed from hello beginning of hello block.</span></span>
* <span data-ttu-id="828a7-158">No puede usar la [ejecución en paralelo](#parallel-processing) dentro de un bloque de InlineScript.</span><span class="sxs-lookup"><span data-stu-id="828a7-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="828a7-159">InlineScript afecta a la escalabilidad de flujo de trabajo de hello ya que retiene la sesión de Windows PowerShell de hello hasta alcanzar la longitud completa Hola del bloque de InlineScript Hola.</span><span class="sxs-lookup"><span data-stu-id="828a7-159">InlineScript affects scalability of hello workflow since it holds hello Windows PowerShell session for hello entire length of hello InlineScript block.</span></span>

<span data-ttu-id="828a7-160">Para más información sobre el uso de InlineScript, vea [Ejecutar comandos de Windows PowerShell en un flujo de trabajo](http://technet.microsoft.com/library/jj574197.aspx) y [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span><span class="sxs-lookup"><span data-stu-id="828a7-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="828a7-161">Procesamiento en paralelo</span><span class="sxs-lookup"><span data-stu-id="828a7-161">Parallel processing</span></span>
<span data-ttu-id="828a7-162">Una ventaja de flujos de trabajo de Windows PowerShell es Hola capacidad tooperform un conjunto de comandos en paralelo en lugar de secuencialmente como con un script típico.</span><span class="sxs-lookup"><span data-stu-id="828a7-162">One advantage of Windows PowerShell Workflows is hello ability tooperform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="828a7-163">Puede usar hello **paralelo** palabra clave toocreate un bloque de script con varios comandos que se ejecutan simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="828a7-163">You can use hello **Parallel** keyword toocreate a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="828a7-164">Esto utiliza Hola sintaxis que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="828a7-164">This uses hello following syntax shown below.</span></span> <span data-ttu-id="828a7-165">En este caso, Activity1 y Activity2 se inicia en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="828a7-165">In this case, Activity1 and Activity2 starts at hello same time.</span></span> <span data-ttu-id="828a7-166">Activity3 se inicia después de que se hayan completado Activity1 y Activity2.</span><span class="sxs-lookup"><span data-stu-id="828a7-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="828a7-167">Por ejemplo, considere la posibilidad de hello siga los comandos de PowerShell que varios archivos tooa red destino de la copia.</span><span class="sxs-lookup"><span data-stu-id="828a7-167">For example, consider hello following PowerShell commands that copy multiple files tooa network destination.</span></span>  <span data-ttu-id="828a7-168">Estos comandos se ejecutan secuencialmente para que un archivo debe finalizar copia antes de Hola a continuación se inicia.</span><span class="sxs-lookup"><span data-stu-id="828a7-168">These commands are run sequentially so that one file must finish copying before hello next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="828a7-169">Hello siguiente flujo de trabajo ejecuta estos mismos comandos en paralelo para que todos ellos comenzarán a copiar Hola mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="828a7-169">hello following workflow runs these same commands in parallel so that they all start copying at hello same time.</span></span>  <span data-ttu-id="828a7-170">Solo después de que todos estén copiados se mensaje de bienvenida de finalización muestra.</span><span class="sxs-lookup"><span data-stu-id="828a7-170">Only after they are all copied is hello completion message displayed.</span></span>

    Workflow Copy-Files
    {
        Parallel
        {
            Copy-Item -Path "C:\LocalPath\File1.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File2.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File3.txt" -Destination "\\NetworkPath"
        }

        Write-Output "Files copied."
    }


<span data-ttu-id="828a7-171">Puede usar hello **ForEach-Parallel** construir comandos tooprocess para cada elemento de una colección simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="828a7-171">You can use hello **ForEach -Parallel** construct tooprocess commands for each item in a collection concurrently.</span></span> <span data-ttu-id="828a7-172">elementos de Hola de colección de Hola se procesan en paralelo mientras comandos Hola Hola bloque de script se ejecutan secuencialmente.</span><span class="sxs-lookup"><span data-stu-id="828a7-172">hello items in hello collection are processed in parallel while hello commands in hello script block run sequentially.</span></span> <span data-ttu-id="828a7-173">Esto utiliza Hola sintaxis que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="828a7-173">This uses hello following syntax shown below.</span></span> <span data-ttu-id="828a7-174">En este caso, Activity1 se inicia en hello la misma hora para todos los elementos de la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="828a7-174">In this case, Activity1 starts at hello same time for all items in hello collection.</span></span> <span data-ttu-id="828a7-175">Para cada elemento, Activity2 se inicia una vez completado Activity1.</span><span class="sxs-lookup"><span data-stu-id="828a7-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="828a7-176">Activity3 se inicia únicamente después de que se hayan completado Activity1 y Activity2 para todos los elementos.</span><span class="sxs-lookup"><span data-stu-id="828a7-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="828a7-177">Hola siguiente ejemplo es similar toohello de ejemplo anterior copiar archivos en paralelo.</span><span class="sxs-lookup"><span data-stu-id="828a7-177">hello following example is similar toohello previous example copying files in parallel.</span></span>  <span data-ttu-id="828a7-178">En este caso, se muestra un mensaje para cada archivo después de copiarse.</span><span class="sxs-lookup"><span data-stu-id="828a7-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="828a7-179">Solo después de que todos estén completamente copiados se mensajes de bienvenida del final de conclusión muestra.</span><span class="sxs-lookup"><span data-stu-id="828a7-179">Only after they are all completely copied is hello final completion message displayed.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach -Parallel ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
        }

        Write-Output "All files copied."
    }

> [!NOTE]
> <span data-ttu-id="828a7-180">No se recomienda ejecutando runbooks secundarios en paralelo, ya que esto ha demostrado toogive de resultados no confiables.</span><span class="sxs-lookup"><span data-stu-id="828a7-180">We do not recommend running child runbooks in parallel since this has been shown toogive unreliable results.</span></span>  <span data-ttu-id="828a7-181">Hello salida del runbook a veces de hello secundario no se muestra, y puede afectar la configuración en un elemento secundario runbook Hola otros runbooks secundarios paralelas</span><span class="sxs-lookup"><span data-stu-id="828a7-181">hello output from hello child runbook sometimes does not show up, and settings in one child runbook can affect hello other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="828a7-182">Puntos de control</span><span class="sxs-lookup"><span data-stu-id="828a7-182">Checkpoints</span></span>
<span data-ttu-id="828a7-183">A *punto de comprobación* es una instantánea del estado actual de Hola de flujo de trabajo de Hola que incluye el valor actual de Hola para las variables y los resultados se punto toothat generado.</span><span class="sxs-lookup"><span data-stu-id="828a7-183">A *checkpoint* is a snapshot of hello current state of hello workflow that includes hello current value for variables and any output generated toothat point.</span></span> <span data-ttu-id="828a7-184">Si un flujo de trabajo termina en error o está suspendido, Hola próxima vez que se ejecute se iniciará desde su último punto de comprobación en lugar de inicio de Hola de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="828a7-184">If a workflow ends in error or is suspended, then hello next time it is run it will start from its last checkpoint instead of hello start of hello worfklow.</span></span>  <span data-ttu-id="828a7-185">Puede establecer un punto de control en un flujo de trabajo con hello **Checkpoint-Workflow** actividad.</span><span class="sxs-lookup"><span data-stu-id="828a7-185">You can set a checkpoint in a workflow with hello **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="828a7-186">En el siguiente código de ejemplo de Hola, se produce una excepción después de Activity2 que produce Hola tooend de flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="828a7-186">In hello following sample code, an exception occurs after Activity2 causing hello workflow tooend.</span></span> <span data-ttu-id="828a7-187">Cuando se vuelve a ejecutar el flujo de trabajo de hello, se inicia ejecutando Activity2, ya que se encontraba justo detrás de hello último punto de control establecido.</span><span class="sxs-lookup"><span data-stu-id="828a7-187">When hello workflow is run again, it starts by running Activity2 since this was just after hello last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="828a7-188">Debe establecer los puntos de comprobación en un flujo de trabajo después de que las actividades que pueden ser propensas a tooexception y no deben repiten si se reanuda el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="828a7-188">You should set checkpoints in a workflow after activities that may be prone tooexception and should not be repeated if hello workflow is resumed.</span></span> <span data-ttu-id="828a7-189">Por ejemplo, el flujo de trabajo puede crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="828a7-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="828a7-190">Puede establecer un punto de control antes y después de la máquina virtual de hello comandos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="828a7-190">You could set a checkpoint both before and after hello commands toocreate hello virtual machine.</span></span> <span data-ttu-id="828a7-191">Si se produce un error en la creación de hello, se repetiría comandos Hola si se inicia el flujo de trabajo de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="828a7-191">If hello creation fails, then hello commands would be repeated if hello workflow is started again.</span></span> <span data-ttu-id="828a7-192">Si se produce un error en el flujo de trabajo de hello después Hola se crea correctamente, a continuación, máquina virtual de hello no se creará nuevo cuando se reanuda el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="828a7-192">If hello worfklow fails after hello creation succeeds, then hello virtual machine will not be created again when hello workflow is resumed.</span></span>

<span data-ttu-id="828a7-193">Hola siguiente ejemplo copia la ubicación de red de varios archivos tooa y establece un punto de control después de cada archivo.</span><span class="sxs-lookup"><span data-stu-id="828a7-193">hello following example copies multiple files tooa network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="828a7-194">Si se pierde la ubicación de red de hello, flujo de trabajo de hello termina en error.</span><span class="sxs-lookup"><span data-stu-id="828a7-194">If hello network location is lost, then hello workflow ends in error.</span></span>  <span data-ttu-id="828a7-195">Cuando se inicia de nuevo, se reanudará en hello último punto de comprobación lo que significa que sólo los archivos de Hola que ya se han copiado se omiten.</span><span class="sxs-lookup"><span data-stu-id="828a7-195">When it is started again, it will resume at hello last checkpoint meaning that only hello files that have already been copied are skipped.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
            Checkpoint-Workflow
        }

        Write-Output "All files copied."
    }

<span data-ttu-id="828a7-196">Puesto que las credenciales de nombre de usuario no se conservan después de llamar a hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) actividad o después de hello último punto de comprobación, necesita tooset Hola credenciales toonull y, a continuación, recuperarlos nuevo desde el almacén de activos de hello después  **Flujo de trabajo suspender** o se denomina punto de comprobación.</span><span class="sxs-lookup"><span data-stu-id="828a7-196">Because username credentials are not persisted after you call hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after hello last checkpoint, you need tooset hello credentials toonull and then retrieve them again from hello asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="828a7-197">En caso contrario, recibirá Hola siguiente mensaje de error: *no se puede reanudar el flujo de trabajo de hello, ya sea porque los datos de persistencia no se pudieron guardar por completo, o guardar datos de persistencia se ha dañado. Debe reiniciar el flujo de trabajo de Hola.*</span><span class="sxs-lookup"><span data-stu-id="828a7-197">Otherwise, you may receive hello following error message: *hello workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart hello workflow.*</span></span>

<span data-ttu-id="828a7-198">Hola siguiendo el mismo código se muestra cómo toohandle esto en sus runbooks de flujo de trabajo de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="828a7-198">hello following same code demonstrates how toohandle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first toocreate hello VM (code not shown)

          # Now add hello VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="828a7-199">Este paso no es necesario si se autentica utilizando una cuenta de ejecución configurada con una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="828a7-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="828a7-200">Para obtener más información acerca de los puntos de control, vea [tooa de puntos de control Agregar flujo de trabajo de Script](http://technet.microsoft.com/library/jj574114.aspx).</span><span class="sxs-lookup"><span data-stu-id="828a7-200">For more information about checkpoints, see [Adding Checkpoints tooa Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="828a7-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="828a7-201">Next steps</span></span>
* <span data-ttu-id="828a7-202">tooget a trabajar con runbooks de flujo de trabajo de PowerShell, consulte [mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="828a7-202">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
