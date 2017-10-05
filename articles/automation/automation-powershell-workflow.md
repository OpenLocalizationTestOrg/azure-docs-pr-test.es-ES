---
title: Aprendizaje del flujo de trabajo de Windows PowerShell para Azure Automation | Microsoft Docs
description: "Este artículo está destinado como una lección rápida para que los autores familiarizados con PowerShell comprendan las diferencias específicas entre Powershell y el flujo de trabajo de PowerShell y los conceptos aplicables a los runbooks de Automation."
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
ms.openlocfilehash: 4de812c7f863e42a6ed10c2312d61b8377e06431
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="e7a9f-103">Aprendizaje de los conceptos básicos del flujo de trabajo de Windows PowerShell para los runbooks de Automation</span><span class="sxs-lookup"><span data-stu-id="e7a9f-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="e7a9f-104">Los runbooks de Azure Automation se implementan como flujos de trabajo de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="e7a9f-105">Un flujo de trabajo de Windows PowerShell es similar a un script de Windows PowerShell, pero presenta algunas diferencias importantes que pueden resultar confusas para un usuario nuevo.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-105">A Windows PowerShell Workflow is similar to a Windows PowerShell script but has some significant differences that can be confusing to a new user.</span></span>  <span data-ttu-id="e7a9f-106">Aunque este artículo está pensado para ayudarle a escribir runbooks con el flujo de trabajo de PowerShell, se recomienda que escribir runbooks con PowerShell, a menos que necesite puntos de control.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-106">While this article is intended to help you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="e7a9f-107">Hay varias diferencias de sintaxis al crear runbooks de flujo de trabajo de PowerShell y estas diferencias requieren algo más de trabajo para escribir flujos de trabajo eficaces.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work to write effective workflows.</span></span>  

<span data-ttu-id="e7a9f-108">Un flujo de trabajo es una secuencia de pasos programados y conectados que realizan tareas de larga duración o requieren la coordinación de varios pasos en varios dispositivos o nodos administrados.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require the coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="e7a9f-109">Las ventajas de un flujo de trabajo en un script normal incluyen la capacidad de realizar una acción en varios dispositivos simultáneamente y la capacidad de recuperarse automáticamente de los errores.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-109">The benefits of a workflow over a normal script include the ability to simultaneously perform an action against multiple devices and the ability to automatically recover from failures.</span></span> <span data-ttu-id="e7a9f-110">Un flujo de trabajo de Windows PowerShell es un script de Windows PowerShell que usa Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="e7a9f-111">Aunque el flujo de trabajo está escrito con sintaxis de Windows PowerShell y se inicia mediante Windows PowerShell, se procesa mediante Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-111">While the workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="e7a9f-112">Para obtener información detallada sobre los temas de este artículo, vea [Introducción al flujo de trabajo de Windows PowerShell](http://technet.microsoft.com/library/jj134242.aspx).</span><span class="sxs-lookup"><span data-stu-id="e7a9f-112">For complete details on the topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="e7a9f-113">Estructura básica de un flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="e7a9f-113">Basic structure of a workflow</span></span>
<span data-ttu-id="e7a9f-114">El primer paso para convertir un script de PowerShell en un flujo de trabajo de PowerShell es delimitarlo con la palabra clave **Workflow** .</span><span class="sxs-lookup"><span data-stu-id="e7a9f-114">The first step to converting a PowerShell script to a PowerShell workflow is enclosing it with the **Workflow** keyword.</span></span>  <span data-ttu-id="e7a9f-115">Un flujo de trabajo comienza con la palabra clave **Workflow** , seguida del cuerpo del script entre llaves.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-115">A workflow starts with the **Workflow** keyword followed by the body of the script enclosed in braces.</span></span> <span data-ttu-id="e7a9f-116">El nombre del flujo de trabajo sigue a la palabra clave **Workflow**, tal como se muestra en la sintaxis siguiente:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-116">The name of the workflow follows the **Workflow** keyword as shown in the following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="e7a9f-117">El nombre del flujo de trabajo debe coincidir con el nombre del runbook de Automation.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-117">The name of the workflow must match the name of the Automation runbook.</span></span> <span data-ttu-id="e7a9f-118">Si se va a importar el runbook, el nombre de archivo debe coincidir con el nombre del flujo de trabajo y debe terminar en *.ps1*.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-118">If the runbook is being imported, then the filename must match the workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="e7a9f-119">Para agregar parámetros al flujo de trabajo, use la palabra clave **Param** palabra clave igual que lo haría para un script.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-119">To add parameters to the workflow, use the **Param** keyword just as you would to a script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="e7a9f-120">Cambios de código</span><span class="sxs-lookup"><span data-stu-id="e7a9f-120">Code changes</span></span>
<span data-ttu-id="e7a9f-121">El código de flujo de trabajo de PowerShell es casi idéntico al código de script de PowerShell salvo por algunos cambios importantes.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-121">PowerShell workflow code looks almost identical to PowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="e7a9f-122">En las secciones siguientes se describen los cambios que debe realizar en un script de PowerShell para que se ejecute en un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-122">The following sections describe changes that you need to make to a PowerShell script for it to run in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="e7a9f-123">Actividades</span><span class="sxs-lookup"><span data-stu-id="e7a9f-123">Activities</span></span>
<span data-ttu-id="e7a9f-124">Una actividad es una tarea específica de un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="e7a9f-125">Al igual que un script se compone de uno o varios comandos, un flujo de trabajo se compone de una o varias actividades que se realizan en secuencia.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="e7a9f-126">El flujo de trabajo de Windows PowerShell convierte automáticamente muchos de los cmdlets de Windows PowerShell en actividades cuando se ejecuta un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-126">Windows PowerShell Workflow automatically converts many of the Windows PowerShell cmdlets to activities when it runs a workflow.</span></span> <span data-ttu-id="e7a9f-127">Cuando se especifica uno de estos cmdlets en el runbook, Windows Workflow Foundation ejecuta la actividad correspondiente.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-127">When you specify one of these cmdlets in your runbook, the corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="e7a9f-128">Para los cmdlets sin actividad correspondiente, el flujo de trabajo de Windows PowerShell ejecuta automáticamente el cmdlet dentro de una actividad [InlineScript](#inlinescript) .</span><span class="sxs-lookup"><span data-stu-id="e7a9f-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs the cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="e7a9f-129">Hay un conjunto de cmdlets que están excluidos y no se pueden usar en un flujo de trabajo a menos que incluya explícitamente en un bloque de InlineScript.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="e7a9f-130">Para obtener más información sobre estos conceptos, consulte [Uso de actividades en los flujos de trabajo de scripts](http://technet.microsoft.com/library/jj574194.aspx).</span><span class="sxs-lookup"><span data-stu-id="e7a9f-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="e7a9f-131">Las actividades de flujo de trabajo comparten un conjunto de parámetros comunes para configurar su funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-131">Workflow activities share a set of common parameters to configure their operation.</span></span> <span data-ttu-id="e7a9f-132">Para más información sobre los parámetros comunes del flujo de trabajo, vea [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="e7a9f-132">For details about the workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="e7a9f-133">Parámetros posicionales</span><span class="sxs-lookup"><span data-stu-id="e7a9f-133">Positional parameters</span></span>
<span data-ttu-id="e7a9f-134">No puede usar parámetros posicionales con actividades y cmdlets en un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="e7a9f-135">Todo esto significa que debe usar nombres de parámetros.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="e7a9f-136">Por ejemplo, considere el siguiente código que obtiene todos los servicios en ejecución.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-136">For example, consider the following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="e7a9f-137">Si intenta ejecutar este mismo código en un flujo de trabajo, obtiene un mensaje parecido a "El conjunto de parámetros no se puede resolver mediante los parámetros con nombre especificados".</span><span class="sxs-lookup"><span data-stu-id="e7a9f-137">If you try to run this same code in a workflow, you receive a message like "Parameter set cannot be resolved using the specified named parameters."</span></span>  <span data-ttu-id="e7a9f-138">Para corregir este problema, proporcione el nombre del parámetro de la forma siguiente.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-138">To correct this, provide the parameter name as in the following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="e7a9f-139">Objetos deserializados</span><span class="sxs-lookup"><span data-stu-id="e7a9f-139">Deserialized objects</span></span>
<span data-ttu-id="e7a9f-140">Los objetos de los flujos de trabajo están deserializados.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="e7a9f-141">Esto significa que sus propiedades siguen estando disponibles, pero no sus métodos.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="e7a9f-142">Por ejemplo, considere el siguiente código de PowerShell que detiene un servicio mediante el método Stop del objeto Service.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-142">For example, consider the following PowerShell code that stops a service using the Stop method of the Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="e7a9f-143">Si intenta ejecutar esto en un flujo de trabajo, obtiene un error que indica "La invocación del método no se admite en un flujo de trabajo de Windows PowerShell".</span><span class="sxs-lookup"><span data-stu-id="e7a9f-143">If you try to run this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="e7a9f-144">Una opción es ajustar estas dos líneas de código en un bloque [InlineScript](#inlinescript), en cuyo caso $Service sería un objeto de servicio dentro del bloque.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-144">One option is to wrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within the block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="e7a9f-145">Otra opción es usar otro cmdlet que realiza la misma funcionalidad que el método, si hay uno disponible.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-145">Another option is to use another cmdlet that performs the same functionality as the method, if one is available.</span></span>  <span data-ttu-id="e7a9f-146">En nuestro ejemplo, el cmdlet Stop-Service proporciona la misma funcionalidad que el método Stop, y podría usar lo siguiente para un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-146">In our sample, the Stop-Service cmdlet provides the same functionality as the Stop method, and you could use the following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="e7a9f-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="e7a9f-147">InlineScript</span></span>
<span data-ttu-id="e7a9f-148">La actividad **InlineScript** es útil cuando necesita ejecutar uno o más comandos tradicional como script tradicional de PowerShell en lugar de como flujo de trabajo de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-148">The **InlineScript** activity is useful when you need to run one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="e7a9f-149">Mientras que los comandos de un flujo de trabajo se envían a Windows Workflow Foundation para su procesamiento, los comandos de un bloque de InlineScript se procesan mediante Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-149">While commands in a workflow are sent to Windows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="e7a9f-150">InlineScript usa la sintaxis que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-150">InlineScript uses the following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="e7a9f-151">Puede devolver resultados de InlineScript asignando el resultado a una variable.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-151">You can return output from an InlineScript by assigning the output to a variable.</span></span> <span data-ttu-id="e7a9f-152">El siguiente ejemplo detiene un servicio y, a continuación, envía el nombre de servicio.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-152">The following example stops a service and then outputs the service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="e7a9f-153">Puede pasar valores en un bloque de InlineScript, pero debe usar el modificador de ámbito **$Using** .</span><span class="sxs-lookup"><span data-stu-id="e7a9f-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="e7a9f-154">El ejemplo siguiente es idéntico al ejemplo anterior salvo que se proporciona el nombre de servicio mediante una variable.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-154">The following example is identical to the previous example except that the service name is provided by a variable.</span></span>

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


<span data-ttu-id="e7a9f-155">Aunque las actividades InlineScript pueden ser críticas en algunos flujos de trabajo, no son compatibles con las construcciones de flujo de trabajo y solo se deben usar cuando sea necesario por las razones siguientes:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for the following reasons:</span></span>

* <span data-ttu-id="e7a9f-156">No puede usar [puntos de comprobación](#checkpoints) dentro de un bloque de InlineScript.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="e7a9f-157">Si se produce un error dentro del bloque, se debe reanudar desde el principio del bloque.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-157">If a failure occurs within the block, it must be resumed from the beginning of the block.</span></span>
* <span data-ttu-id="e7a9f-158">No puede usar la [ejecución en paralelo](#parallel-processing) dentro de un bloque de InlineScript.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="e7a9f-159">InlineScript afecta a la escalabilidad del flujo de trabajo, ya que retiene la sesión de Windows PowerShell durante todo el bloque de InlineScript.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-159">InlineScript affects scalability of the workflow since it holds the Windows PowerShell session for the entire length of the InlineScript block.</span></span>

<span data-ttu-id="e7a9f-160">Para más información sobre el uso de InlineScript, vea [Ejecutar comandos de Windows PowerShell en un flujo de trabajo](http://technet.microsoft.com/library/jj574197.aspx) y [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span><span class="sxs-lookup"><span data-stu-id="e7a9f-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="e7a9f-161">Procesamiento en paralelo</span><span class="sxs-lookup"><span data-stu-id="e7a9f-161">Parallel processing</span></span>
<span data-ttu-id="e7a9f-162">Una ventaja de los flujos de trabajo de Windows PowerShell es la capacidad para realizar un conjunto de comandos en paralelo en lugar de hacerlo secuencialmente como con un script típico.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-162">One advantage of Windows PowerShell Workflows is the ability to perform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="e7a9f-163">Puede usar la palabra clave **Parallel** para crear un bloque de scripts con varios comandos que se ejecuten simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-163">You can use the **Parallel** keyword to create a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="e7a9f-164">Esto usa la siguiente sintaxis que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-164">This uses the following syntax shown below.</span></span> <span data-ttu-id="e7a9f-165">En este caso, Activity1 y Activity2 se inician al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-165">In this case, Activity1 and Activity2 starts at the same time.</span></span> <span data-ttu-id="e7a9f-166">Activity3 se inicia después de que se hayan completado Activity1 y Activity2.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="e7a9f-167">Por ejemplo, considere los siguientes comandos de PowerShell que copian varios archivos a un destino de red.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-167">For example, consider the following PowerShell commands that copy multiple files to a network destination.</span></span>  <span data-ttu-id="e7a9f-168">Estos comandos se ejecutan secuencialmente de modo que un archivo debe terminar de copiarse antes de que comience el siguiente.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-168">These commands are run sequentially so that one file must finish copying before the next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="e7a9f-169">El flujo de trabajo siguiente ejecuta estos mismos comandos en paralelo para que todos ellos empiezan a copiarse al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-169">The following workflow runs these same commands in parallel so that they all start copying at the same time.</span></span>  <span data-ttu-id="e7a9f-170">Una vez que todos se han copiado, se muestra el mensaje de finalización.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-170">Only after they are all copied is the completion message displayed.</span></span>

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


<span data-ttu-id="e7a9f-171">Puede utilizar la construcción **ForEach-Parallel** para procesar comandos para cada elemento de una colección simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-171">You can use the **ForEach -Parallel** construct to process commands for each item in a collection concurrently.</span></span> <span data-ttu-id="e7a9f-172">Los elementos de la colección se procesan en paralelo mientras que los comandos del bloque de scripts se ejecutan secuencialmente.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-172">The items in the collection are processed in parallel while the commands in the script block run sequentially.</span></span> <span data-ttu-id="e7a9f-173">Esto usa la siguiente sintaxis que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-173">This uses the following syntax shown below.</span></span> <span data-ttu-id="e7a9f-174">En este caso, Activity1 se inicia al mismo tiempo para todos los elementos de la colección.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-174">In this case, Activity1 starts at the same time for all items in the collection.</span></span> <span data-ttu-id="e7a9f-175">Para cada elemento, Activity2 se inicia una vez completado Activity1.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="e7a9f-176">Activity3 se inicia únicamente después de que se hayan completado Activity1 y Activity2 para todos los elementos.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="e7a9f-177">El ejemplo siguiente es similar al ejemplo anterior, en el que se copian archivos en paralelo.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-177">The following example is similar to the previous example copying files in parallel.</span></span>  <span data-ttu-id="e7a9f-178">En este caso, se muestra un mensaje para cada archivo después de copiarse.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="e7a9f-179">Solo después de que todos se hayan copiado completamente, aparecerá el mensaje de finalización.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-179">Only after they are all completely copied is the final completion message displayed.</span></span>

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
> <span data-ttu-id="e7a9f-180">No se recomienda ejecutar runbooks secundarios en paralelo, ya que se ha demostrado que no tiene unos resultados confiables.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-180">We do not recommend running child runbooks in parallel since this has been shown to give unreliable results.</span></span>  <span data-ttu-id="e7a9f-181">A veces el resultado del runbook secundario no se muestra, y la configuración de un runbook secundario puede afectar a los demás runbooks secundarios paralelos.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-181">The output from the child runbook sometimes does not show up, and settings in one child runbook can affect the other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="e7a9f-182">puntos de comprobación</span><span class="sxs-lookup"><span data-stu-id="e7a9f-182">Checkpoints</span></span>
<span data-ttu-id="e7a9f-183">Un *punto de control* es una instantánea del estado actual del flujo de trabajo que incluye el valor actual de las variables y cualquier salida generada en ese punto.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-183">A *checkpoint* is a snapshot of the current state of the workflow that includes the current value for variables and any output generated to that point.</span></span> <span data-ttu-id="e7a9f-184">Si un flujo de trabajo termina en error o se suspende, la próxima vez que se ejecute comenzará desde su último punto de comprobación, en lugar de desde el inicio del flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-184">If a workflow ends in error or is suspended, then the next time it is run it will start from its last checkpoint instead of the start of the worfklow.</span></span>  <span data-ttu-id="e7a9f-185">Puede establecer un punto de control en un flujo de trabajo con la actividad **Checkpoint-Workflow** .</span><span class="sxs-lookup"><span data-stu-id="e7a9f-185">You can set a checkpoint in a workflow with the **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="e7a9f-186">En el código de ejemplo siguiente, se produce una excepción después de Activity2 que provoca la finalización del flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-186">In the following sample code, an exception occurs after Activity2 causing the workflow to end.</span></span> <span data-ttu-id="e7a9f-187">Cuando se vuelve a ejecutar el flujo de trabajo, se inicia ejecutando Activity2, ya que estaba justo después del último punto de comprobación establecido.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-187">When the workflow is run again, it starts by running Activity2 since this was just after the last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="e7a9f-188">Debe establecer los puntos de comprobación en un flujo de trabajo después de las actividades que puedan ser propensas a la excepción y que no deben repetirse si se reanuda el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-188">You should set checkpoints in a workflow after activities that may be prone to exception and should not be repeated if the workflow is resumed.</span></span> <span data-ttu-id="e7a9f-189">Por ejemplo, el flujo de trabajo puede crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="e7a9f-190">Puede establecer un punto de control antes y después de los comandos para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-190">You could set a checkpoint both before and after the commands to create the virtual machine.</span></span> <span data-ttu-id="e7a9f-191">Si se produce un error en la creación,  los comandos se repetirían si el flujo de trabajo se vuelve a iniciar.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-191">If the creation fails, then the commands would be repeated if the workflow is started again.</span></span> <span data-ttu-id="e7a9f-192">Si el flujo de trabajo produce un error después de que la creación se haya realizado correctamente, la máquina virtual no se volverá a crear cuando se reanude el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-192">If the worfklow fails after the creation succeeds, then the virtual machine will not be created again when the workflow is resumed.</span></span>

<span data-ttu-id="e7a9f-193">El siguiente ejemplo copia varios archivos en una ubicación de red y establece un punto de comprobación después de cada archivo.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-193">The following example copies multiple files to a network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="e7a9f-194">Si la ubicación de red se pierde, el flujo de trabajo finaliza con error.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-194">If the network location is lost, then the workflow ends in error.</span></span>  <span data-ttu-id="e7a9f-195">Cuando se vuelva a iniciar, se reanudará en el último punto de comprobación, lo que significa que solo se omiten los archivos que ya se han copiado.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-195">When it is started again, it will resume at the last checkpoint meaning that only the files that have already been copied are skipped.</span></span>

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

<span data-ttu-id="e7a9f-196">Como las credenciales de nombre de usuario no se conservan después de llamar a la actividad [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) o del último punto de control, necesita establecer las credenciales en NULL y, después, recuperarlas de nuevo desde el almacén de recursos tras llamar a **Suspend-Workflow** o al punto de control.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-196">Because username credentials are not persisted after you call the [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after the last checkpoint, you need to set the credentials to null and then retrieve them again from the asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="e7a9f-197">De lo contrario, puede que reciba el siguiente mensaje de error: *No puede reanudarse el trabajo de flujo de trabajo dado que no se pudieron guardar los datos de persistencia completamente o dichos datos estaban dañados. Debe reiniciar el flujo de trabajo.*</span><span class="sxs-lookup"><span data-stu-id="e7a9f-197">Otherwise, you may receive the following error message: *The workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart the workflow.*</span></span>

<span data-ttu-id="e7a9f-198">El mismo código de abajo muestra cómo controlar esta operación en los Runbooks del flujo de trabajo de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-198">The following same code demonstrates how to handle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first to create the VM (code not shown)

          # Now add the VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="e7a9f-199">Este paso no es necesario si se autentica utilizando una cuenta de ejecución configurada con una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="e7a9f-200">Para obtener más información acerca de los puntos de control, consulte [Adición de puntos de control a un flujo de trabajo de scripts](http://technet.microsoft.com/library/jj574114.aspx).</span><span class="sxs-lookup"><span data-stu-id="e7a9f-200">For more information about checkpoints, see [Adding Checkpoints to a Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7a9f-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e7a9f-201">Next steps</span></span>
* <span data-ttu-id="e7a9f-202">Para empezar a trabajar con Runbooks de flujo de trabajo de PowerShell, consulte [Mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="e7a9f-202">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
