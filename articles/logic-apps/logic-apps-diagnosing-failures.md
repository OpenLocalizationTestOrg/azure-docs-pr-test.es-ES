---
title: "Diagnóstico de errores: Azure Logic Apps | Microsoft Docs"
description: "Maneras comunes de identificar dónde se producen los errores en las aplicaciones lógicas"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 814e6f93088cdd96b0a663d2a7494b5a11470d99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="05b8f-103">Diagnóstico de errores en las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="05b8f-103">Diagnose logic app failures</span></span>
<span data-ttu-id="05b8f-104">Si surgen problemas o errores con las aplicaciones lógicas, puede adoptar varios enfoques para conocer mejor su origen.</span><span class="sxs-lookup"><span data-stu-id="05b8f-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where the failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="05b8f-105">Herramientas del Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="05b8f-105">Azure portal tools</span></span>
<span data-ttu-id="05b8f-106">El Portal de Azure proporciona muchas herramientas para diagnosticar todas las aplicaciones lógicas en cada paso.</span><span class="sxs-lookup"><span data-stu-id="05b8f-106">The Azure portal provides many tools to diagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="05b8f-107">Historial de desencadenamiento</span><span class="sxs-lookup"><span data-stu-id="05b8f-107">Trigger history</span></span>

<span data-ttu-id="05b8f-108">Cada aplicación lógica tiene al menos un desencadenador.</span><span class="sxs-lookup"><span data-stu-id="05b8f-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="05b8f-109">Si observa que las aplicaciones no se activan, para más información, busque primero en el historial de desencadenadores,</span><span class="sxs-lookup"><span data-stu-id="05b8f-109">If you notice that apps aren't firing, look first at the trigger history for more information.</span></span> <span data-ttu-id="05b8f-110">al cual se accede desde la hoja principal de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="05b8f-110">You can access the trigger history on the logic app'ss main blade.</span></span>

![Ubicación del historial de desencadenamiento][1]

<span data-ttu-id="05b8f-112">En el historial de desencadenadores se enumeran todos los intentos de desencadenamiento de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="05b8f-112">The trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="05b8f-113">Puede hacer clic en ellos para conocer los detalles, en concreto, las entradas o salidas generadas por el intento de desencadenamiento.</span><span class="sxs-lookup"><span data-stu-id="05b8f-113">You can click each trigger attempt to drill into the details, specifically, any inputs or outputs that the trigger attempt generated.</span></span> <span data-ttu-id="05b8f-114">Si encuentra errores en los desencadenadores, seleccione el intento de desencadenamiento y elija el vínculo **Salidas** para revisar los mensajes de error generados, por ejemplo, credenciales de FTP no válidas.</span><span class="sxs-lookup"><span data-stu-id="05b8f-114">If you find failed triggers, select the trigger attempt and choose the **Outputs** link to review any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="05b8f-115">Estos son los diferentes estados que puede ver:</span><span class="sxs-lookup"><span data-stu-id="05b8f-115">The different statuses you might see are:</span></span>

* <span data-ttu-id="05b8f-116">**Omitido**.</span><span class="sxs-lookup"><span data-stu-id="05b8f-116">**Skipped**.</span></span> <span data-ttu-id="05b8f-117">Se sondeó el punto de conexión para buscar datos y se recibió como respuesta que no había datos disponibles.</span><span class="sxs-lookup"><span data-stu-id="05b8f-117">The endpoint was polled to check for data and received a response that no data was available.</span></span>
* <span data-ttu-id="05b8f-118">**Correcto**.</span><span class="sxs-lookup"><span data-stu-id="05b8f-118">**Succeeded**.</span></span> <span data-ttu-id="05b8f-119">El desencadenador recibió como respuesta que los datos estaban disponibles.</span><span class="sxs-lookup"><span data-stu-id="05b8f-119">The trigger received a response that data was available.</span></span> <span data-ttu-id="05b8f-120">Este estado podría proceder de un desencadenador manual, uno de periodicidad o uno de sondeo.</span><span class="sxs-lookup"><span data-stu-id="05b8f-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="05b8f-121">Suele ir acompañado de un estado **desencadenado**, pero puede no ser así si tiene una condición o un comando SplitOn en la vista de código que no se haya satisfecho.</span><span class="sxs-lookup"><span data-stu-id="05b8f-121">This status is usually accompanied by the **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="05b8f-122">**Error**.</span><span class="sxs-lookup"><span data-stu-id="05b8f-122">**Failed**.</span></span> <span data-ttu-id="05b8f-123">Se generó un error.</span><span class="sxs-lookup"><span data-stu-id="05b8f-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="05b8f-124">Inicio manual de un desencadenador</span><span class="sxs-lookup"><span data-stu-id="05b8f-124">Start a trigger manually</span></span>

<span data-ttu-id="05b8f-125">Si desea que la aplicación lógica compruebe si hay algún desencadenador disponible de inmediato (sin esperar a la siguiente repetición), haga clic el botón **Seleccionar un desencadenador** en la hoja principal para forzar una comprobación.</span><span class="sxs-lookup"><span data-stu-id="05b8f-125">If you want the logic app to check for an available trigger immediately without waiting for the next recurrence, click **Select Trigger** on the main blade to force a check.</span></span> <span data-ttu-id="05b8f-126">Por ejemplo, al hacer clic en este vínculo con un desencadenador de Dropbox, provocará que el flujo de trabajo sondee Dropbox inmediatamente en busca de archivos nuevos.</span><span class="sxs-lookup"><span data-stu-id="05b8f-126">For example, clicking this link with a Dropbox trigger causes the workflow to immediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="05b8f-127">Historial de ejecuciones</span><span class="sxs-lookup"><span data-stu-id="05b8f-127">Run history</span></span>

<span data-ttu-id="05b8f-128">Cada desencadenador que se activa produce una ejecución.</span><span class="sxs-lookup"><span data-stu-id="05b8f-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="05b8f-129">Puede acceder a información de la ejecución desde la hoja principal, que contiene numerosos detalles útiles para comprender lo sucedido durante el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="05b8f-129">You can access run information from the main blade, which contains many details that can help you understand what happened during the workflow.</span></span>

![Ubicación del historial de ejecuciones][2]

<span data-ttu-id="05b8f-131">Una ejecución muestra uno de los siguientes estados:</span><span class="sxs-lookup"><span data-stu-id="05b8f-131">A run displays one of the following statuses:</span></span>

* <span data-ttu-id="05b8f-132">**Correcto**.</span><span class="sxs-lookup"><span data-stu-id="05b8f-132">**Succeeded**.</span></span> <span data-ttu-id="05b8f-133">Todas las acciones correctas.</span><span class="sxs-lookup"><span data-stu-id="05b8f-133">All actions succeeded.</span></span> <span data-ttu-id="05b8f-134">Si se produjo un error, este se corrigió mediante una acción posterior del flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="05b8f-134">If a failure happened, that failure was handled by an action that occurred later in the workflow.</span></span> <span data-ttu-id="05b8f-135">Es decir, el error se corrigió con una acción que se configuró para ejecutarse después de una acción con error.</span><span class="sxs-lookup"><span data-stu-id="05b8f-135">That is, the failure was handled by an action that was set to run after a failed action.</span></span>
* <span data-ttu-id="05b8f-136">**Error**.</span><span class="sxs-lookup"><span data-stu-id="05b8f-136">**Failed**.</span></span> <span data-ttu-id="05b8f-137">Se produjo un error en al menos una acción que no se controló mediante una acción posteriormente en el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="05b8f-137">At least one action had a failure that was not handled by an action later in the workflow.</span></span>
* <span data-ttu-id="05b8f-138">**Cancelado**.</span><span class="sxs-lookup"><span data-stu-id="05b8f-138">**Cancelled**.</span></span> <span data-ttu-id="05b8f-139">El flujo de trabajo se estaba ejecutando pero recibió una solicitud de cancelación.</span><span class="sxs-lookup"><span data-stu-id="05b8f-139">The workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="05b8f-140">**En ejecución**.</span><span class="sxs-lookup"><span data-stu-id="05b8f-140">**Running**.</span></span> <span data-ttu-id="05b8f-141">El flujo de trabajo se ejecuta actualmente.</span><span class="sxs-lookup"><span data-stu-id="05b8f-141">The workflow is currently running.</span></span> <span data-ttu-id="05b8f-142">Este estado puede darse en flujos de trabajo con limitaciones o a causa del plan de precios actual.</span><span class="sxs-lookup"><span data-stu-id="05b8f-142">This status might occur for throttled workflows, or because of the current pricing plan.</span></span> <span data-ttu-id="05b8f-143">Para conocer los detalles, consulte [los límites de las acciones en la página de precios](https://azure.microsoft.com/pricing/details/app-service/plans/).</span><span class="sxs-lookup"><span data-stu-id="05b8f-143">For details, see [action limits on the pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="05b8f-144">La configuración del diagnóstico (los gráficos que figuran a continuación del historial de ejecución) también proporcionan información sobre los eventos de limitación que se están produciendo.</span><span class="sxs-lookup"><span data-stu-id="05b8f-144">Configuring diagnostics (the charts that appear under the run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="05b8f-145">Cuando se encuentre ante un historial de ejecución, puede profundizar en él para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="05b8f-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="05b8f-146">Salidas del desencadenador</span><span class="sxs-lookup"><span data-stu-id="05b8f-146">Trigger outputs</span></span>

<span data-ttu-id="05b8f-147">Las salidas del desencadenador muestran los datos que se han recibido del desencadenador.</span><span class="sxs-lookup"><span data-stu-id="05b8f-147">Trigger outputs show the data that came from the trigger.</span></span> <span data-ttu-id="05b8f-148">Estas salidas pueden ayudarle a determinar si se devolvieron todas las propiedades según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="05b8f-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="05b8f-149">Si ve cualquier contenido que no conozca, aprenda cómo Azure Logic Apps [administra distintos tipos de contenido](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="05b8f-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![Ejemplos de salidas del desencadenador][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="05b8f-151">Entradas y salidas de acciones</span><span class="sxs-lookup"><span data-stu-id="05b8f-151">Action inputs and outputs</span></span>

<span data-ttu-id="05b8f-152">Puede profundizar en las entradas y salidas que recibió una acción.</span><span class="sxs-lookup"><span data-stu-id="05b8f-152">You can drill into the inputs and outputs that an action received.</span></span> <span data-ttu-id="05b8f-153">Estos datos resultan útiles para conocer el tamaño y la forma de las salidas, así como para encontrar los mensajes de error que se han generado.</span><span class="sxs-lookup"><span data-stu-id="05b8f-153">This data is useful for understanding the size and shape of the outputs, and also for finding any error messages that might have been generated.</span></span>

![Entradas y salidas de acciones][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="05b8f-155">Depuración del flujo de trabajo en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="05b8f-155">Debug workflow runtime</span></span>

<span data-ttu-id="05b8f-156">Además de supervisar las entradas, las salidas y los desencadenadores de una ejecución, puede agregar algunos pasos al flujo de trabajo para facilitar la depuración.</span><span class="sxs-lookup"><span data-stu-id="05b8f-156">Along with monitoring the inputs, outputs, and triggers of a run, you could add some steps to a workflow that help with debugging.</span></span> 
<span data-ttu-id="05b8f-157">[RequestBin](http://requestb.in) .</span><span class="sxs-lookup"><span data-stu-id="05b8f-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="05b8f-158">Mediante el uso de RequestBin, puede configurar un inspector de la solicitud HTTP para determinar el tamaño exacto, la forma y el formato de una solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="05b8f-158">By using RequestBin, you can set up an HTTP request inspector to determine the exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="05b8f-159">Puede crear una herramienta RequestBin y pegar la dirección URL en una acción HTTP POST de aplicación lógica junto con el contenido del cuerpo que desee probar, como una expresión, la salida de otro paso, etc.</span><span class="sxs-lookup"><span data-stu-id="05b8f-159">You can create a RequestBin and paste the URL in a logic app HTTP POST action with body content that you want to test, for example, an expression or another step output.</span></span> <span data-ttu-id="05b8f-160">Después de ejecutar la aplicación lógica puede actualizar RequestBin para ver cómo se formó la solicitud cuando se generó desde el motor de Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="05b8f-160">After you run the logic app, you can refresh your RequestBin to see how the request was formed when generated from the Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
