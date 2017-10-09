---
title: "errores de aaaDiagnose: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Toounderstand de formas comunes que se producen errores en las aplicaciones lógicas"
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
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="ddcd3-103">Diagnóstico de errores en las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="ddcd3-103">Diagnose logic app failures</span></span>
<span data-ttu-id="ddcd3-104">Si experimenta problemas o errores con las aplicaciones lógicas, hay algunos enfoques puede ayudarle a entender mejor dónde proceden los errores de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where hello failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="ddcd3-105">Herramientas del Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ddcd3-105">Azure portal tools</span></span>
<span data-ttu-id="ddcd3-106">Hola portal de Azure proporciona muchos toodiagnose herramientas cada aplicación lógica en cada paso.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-106">hello Azure portal provides many tools toodiagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="ddcd3-107">Historial de desencadenamiento</span><span class="sxs-lookup"><span data-stu-id="ddcd3-107">Trigger history</span></span>

<span data-ttu-id="ddcd3-108">Cada aplicación lógica tiene al menos un desencadenador.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="ddcd3-109">Si observa que las aplicaciones no están activación, buscan primero en el historial de desencadenador de Hola para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-109">If you notice that apps aren't firing, look first at hello trigger history for more information.</span></span> <span data-ttu-id="ddcd3-110">Puede tener acceso a historial de desencadenador de hello en la hoja principal de hello lógica app'ss.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-110">You can access hello trigger history on hello logic app'ss main blade.</span></span>

![Historial de desencadenador de localización Hola][1]

<span data-ttu-id="ddcd3-112">el historial de desencadenador de Hello enumera todos los intentos de desencadenador que realizan la lógica de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-112">hello trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="ddcd3-113">Puede hacer clic en cada toodrill de intento de desencadenador en los detalles de hello, en concreto, cualquier entradas o salidas que Hola intento de desencadenador generan.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-113">You can click each trigger attempt toodrill into hello details, specifically, any inputs or outputs that hello trigger attempt generated.</span></span> <span data-ttu-id="ddcd3-114">Si encuentra errores desencadenadores, seleccione el intento de desencadenador de Hola y elija hello **salidas** vincular tooreview cualquier error generado mensajes, por ejemplo, las credenciales de FTP que no son válidas.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-114">If you find failed triggers, select hello trigger attempt and choose hello **Outputs** link tooreview any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="ddcd3-115">Hola estados diferentes es posible que vea son:</span><span class="sxs-lookup"><span data-stu-id="ddcd3-115">hello different statuses you might see are:</span></span>

* <span data-ttu-id="ddcd3-116">**Omitido**.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-116">**Skipped**.</span></span> <span data-ttu-id="ddcd3-117">punto de conexión de Hello era toocheck sondeo para los datos y recibe una respuesta que no había disponibles datos.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-117">hello endpoint was polled toocheck for data and received a response that no data was available.</span></span>
* <span data-ttu-id="ddcd3-118">**Correcto**.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-118">**Succeeded**.</span></span> <span data-ttu-id="ddcd3-119">desencadenador de Hello recibió una respuesta que los datos estuvieran disponibles.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-119">hello trigger received a response that data was available.</span></span> <span data-ttu-id="ddcd3-120">Este estado podría proceder de un desencadenador manual, uno de periodicidad o uno de sondeo.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="ddcd3-121">Este estado suele ir acompañado hello **inicia** estado, pero podría no ser si tiene una condición o un comando de SplitOn en la vista de código que no se cumple.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-121">This status is usually accompanied by hello **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="ddcd3-122">**Error**.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-122">**Failed**.</span></span> <span data-ttu-id="ddcd3-123">Se generó un error.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="ddcd3-124">Inicio manual de un desencadenador</span><span class="sxs-lookup"><span data-stu-id="ddcd3-124">Start a trigger manually</span></span>

<span data-ttu-id="ddcd3-125">Si desea toocheck de aplicación lógica de Hola para un desencadenador disponible inmediatamente sin esperar la siguiente periodicidad de hello, haga clic en **Seleccionar desencadenador** en hello hoja principal tooforce una comprobación.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-125">If you want hello logic app toocheck for an available trigger immediately without waiting for hello next recurrence, click **Select Trigger** on hello main blade tooforce a check.</span></span> <span data-ttu-id="ddcd3-126">Por ejemplo, al hacer clic en este vínculo con un desencadenador de Dropbox hace que el sondeo de tooimmediately de flujo de trabajo de hello Dropbox para los nuevos archivos.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-126">For example, clicking this link with a Dropbox trigger causes hello workflow tooimmediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="ddcd3-127">Historial de ejecuciones</span><span class="sxs-lookup"><span data-stu-id="ddcd3-127">Run history</span></span>

<span data-ttu-id="ddcd3-128">Cada desencadenador que se activa produce una ejecución.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="ddcd3-129">Puede tener acceso a información de la ejecución de la hoja principal de hello, que contiene muchos detalles que pueden ayudarle a entender qué ha sucedido durante el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-129">You can access run information from hello main blade, which contains many details that can help you understand what happened during hello workflow.</span></span>

![Buscar Hola historial de ejecución][2]

<span data-ttu-id="ddcd3-131">Una ejecución de muestra uno de hello siguientes estados:</span><span class="sxs-lookup"><span data-stu-id="ddcd3-131">A run displays one of hello following statuses:</span></span>

* <span data-ttu-id="ddcd3-132">**Correcto**.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-132">**Succeeded**.</span></span> <span data-ttu-id="ddcd3-133">Todas las acciones correctas.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-133">All actions succeeded.</span></span> <span data-ttu-id="ddcd3-134">Si se produjo un error, dicho error se controlaba mediante una acción que se ha producido más adelante en el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-134">If a failure happened, that failure was handled by an action that occurred later in hello workflow.</span></span> <span data-ttu-id="ddcd3-135">Es decir, error de Hola se controlaba mediante una acción que se estableció toorun después de una acción de error.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-135">That is, hello failure was handled by an action that was set toorun after a failed action.</span></span>
* <span data-ttu-id="ddcd3-136">**Error**.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-136">**Failed**.</span></span> <span data-ttu-id="ddcd3-137">Al menos una acción ha producido un error en el que no estaba controlado por una acción más adelante en el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-137">At least one action had a failure that was not handled by an action later in hello workflow.</span></span>
* <span data-ttu-id="ddcd3-138">**Cancelado**.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-138">**Cancelled**.</span></span> <span data-ttu-id="ddcd3-139">flujo de trabajo de Hola se estaba ejecutando pero recibió una solicitud de cancelación.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-139">hello workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="ddcd3-140">**En ejecución**.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-140">**Running**.</span></span> <span data-ttu-id="ddcd3-141">flujo de trabajo de saludo se está ejecutando actualmente.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-141">hello workflow is currently running.</span></span> <span data-ttu-id="ddcd3-142">Este estado podría producirse para flujos de trabajo limitadas, o debido a Hola actual de plan de precios.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-142">This status might occur for throttled workflows, or because of hello current pricing plan.</span></span> <span data-ttu-id="ddcd3-143">Para obtener más información, consulte [límites de acción en la página de precios de hello](https://azure.microsoft.com/pricing/details/app-service/plans/).</span><span class="sxs-lookup"><span data-stu-id="ddcd3-143">For details, see [action limits on hello pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="ddcd3-144">Configuración de diagnósticos (gráficos de Hola que aparecen en el historial de ejecución de hello) también puede proporcionar información sobre los eventos de limitación que se producen.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-144">Configuring diagnostics (hello charts that appear under hello run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="ddcd3-145">Cuando se encuentre ante un historial de ejecución, puede profundizar en él para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="ddcd3-146">Salidas del desencadenador</span><span class="sxs-lookup"><span data-stu-id="ddcd3-146">Trigger outputs</span></span>

<span data-ttu-id="ddcd3-147">Desencadenador genera mostrar datos de Hola que proceden de desencadenador de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-147">Trigger outputs show hello data that came from hello trigger.</span></span> <span data-ttu-id="ddcd3-148">Estas salidas pueden ayudarle a determinar si se devolvieron todas las propiedades según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="ddcd3-149">Si ve cualquier contenido que no conozca, aprenda cómo Azure Logic Apps [administra distintos tipos de contenido](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="ddcd3-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![Ejemplos de salidas del desencadenador][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="ddcd3-151">Entradas y salidas de acciones</span><span class="sxs-lookup"><span data-stu-id="ddcd3-151">Action inputs and outputs</span></span>

<span data-ttu-id="ddcd3-152">Puede profundizar en hello entradas y salidas que recibió de una acción.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-152">You can drill into hello inputs and outputs that an action received.</span></span> <span data-ttu-id="ddcd3-153">Estos datos son útiles para entender el tamaño de Hola y la forma de salidas de Hola y también para buscar los mensajes de error que se han generado.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-153">This data is useful for understanding hello size and shape of hello outputs, and also for finding any error messages that might have been generated.</span></span>

![Entradas y salidas de acciones][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="ddcd3-155">Depuración del flujo de trabajo en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="ddcd3-155">Debug workflow runtime</span></span>

<span data-ttu-id="ddcd3-156">Junto con la supervisión Hola entradas, salidas y desencadenadores de una ejecución, puede agregar algunos flujos de trabajo de tooa de pasos que ayudan a depurar.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-156">Along with monitoring hello inputs, outputs, and triggers of a run, you could add some steps tooa workflow that help with debugging.</span></span> 
<span data-ttu-id="ddcd3-157">[RequestBin](http://requestb.in) .</span><span class="sxs-lookup"><span data-stu-id="ddcd3-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="ddcd3-158">Mediante el uso de RequestBin, puede configurar un tamaño exacto de HTTP solicitud inspector toodetermine hello, la forma y el formato de una solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-158">By using RequestBin, you can set up an HTTP request inspector toodetermine hello exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="ddcd3-159">Puede crear un RequestBin y pegue la URL de hello en una aplicación de lógica acción HTTP POST con el contenido del cuerpo que desee tootest, por ejemplo, una expresión o salida del paso de otro.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-159">You can create a RequestBin and paste hello URL in a logic app HTTP POST action with body content that you want tootest, for example, an expression or another step output.</span></span> <span data-ttu-id="ddcd3-160">Después de ejecutar la aplicación de la lógica de hello, puede actualizar su toosee RequestBin cómo se formó solicitud hello cuando genera desde el motor de hello Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="ddcd3-160">After you run hello logic app, you can refresh your RequestBin toosee how hello request was formed when generated from hello Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
