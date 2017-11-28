---
title: "aaaAdd condiciones e iniciar flujos de trabajo: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Controle la ejecución de flujos de trabajo en Azure Logic Apps mediante la incorporación de lógica condicional, desencadenadores, acciones y parámetros."
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="844c9-103">Uso de las características de aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="844c9-103">Use Logic Apps features</span></span>

<span data-ttu-id="844c9-104">En un [tema anterior](../logic-apps/logic-apps-create-a-logic-app.md), creó su primera aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="844c9-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="844c9-105">toocontrol flujo de trabajo de la aplicación lógica, puede especificar diferentes rutas de acceso para su toorun de aplicación lógica y cómo demasiado procesar datos en las matrices, colecciones y lotes.</span><span class="sxs-lookup"><span data-stu-id="844c9-105">toocontrol your logic app's workflow, you can specify different paths for your logic app toorun and how too process data in arrays, collections, and batches.</span></span> <span data-ttu-id="844c9-106">Puede incluir estos elementos en el flujo de trabajo de la aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="844c9-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="844c9-107">Las condiciones y las instrucciones [switch](../logic-apps/logic-apps-switch-case.md) permiten que la aplicación lógica ejecute distintas acciones en función de que se cumplan determinadas condiciones.</span><span class="sxs-lookup"><span data-stu-id="844c9-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="844c9-108">Los [bucles](../logic-apps/logic-apps-loops-and-scopes.md) permiten que la aplicación lógica ejecute pasos varias veces.</span><span class="sxs-lookup"><span data-stu-id="844c9-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="844c9-109">Por ejemplo, puede repetir acciones en una matriz si usa un bucle **For_each**.</span><span class="sxs-lookup"><span data-stu-id="844c9-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="844c9-110">También puede repetir acciones hasta que se cumpla una condición si usa un bucle **Until**.</span><span class="sxs-lookup"><span data-stu-id="844c9-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="844c9-111">[Ámbitos](../logic-apps/logic-apps-loops-and-scopes.md) permiten agrupar serie de acciones juntos, por ejemplo, control de excepciones de tooimplement.</span><span class="sxs-lookup"><span data-stu-id="844c9-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, tooimplement exception handling.</span></span>

* <span data-ttu-id="844c9-112">[Anulando](../logic-apps/logic-apps-loops-and-scopes.md) permite que la aplicación lógica iniciar flujos de trabajo independientes para los elementos en una matriz cuando se usa hello **SplitOn** comando.</span><span class="sxs-lookup"><span data-stu-id="844c9-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use hello **SplitOn** command.</span></span>

<span data-ttu-id="844c9-113">En este tema se presentan otros conceptos de creación de la aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="844c9-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="844c9-114">Vista tooedit una aplicación existente de la lógica de código</span><span class="sxs-lookup"><span data-stu-id="844c9-114">Code view tooedit an existing logic app</span></span>
* <span data-ttu-id="844c9-115">Opciones para iniciar un flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="844c9-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="844c9-116">Condiciones: ejecutan pasos solo después de que se cumpla una condición</span><span class="sxs-lookup"><span data-stu-id="844c9-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="844c9-117">toohave la aplicación lógica ejecutar pasos solo cuando los datos cumplen determinados criterios, puede agregar una condición que compara los datos de flujo de trabajo de hello en campos específicos o valores.</span><span class="sxs-lookup"><span data-stu-id="844c9-117">toohave your logic app run steps only when data meets specific criteria, you can add a condition that compares data in hello workflow against specific fields or values.</span></span>

<span data-ttu-id="844c9-118">Por ejemplo, suponga que tiene una aplicación lógica que le envía demasiados correos electrónicos para entradas en la fuente RSS de un sitio web.</span><span class="sxs-lookup"><span data-stu-id="844c9-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="844c9-119">Puede agregar una condición para que la aplicación lógica envía correo electrónico únicamente cuando Hola de nuevo registrar pertenece tooa determinada categoría.</span><span class="sxs-lookup"><span data-stu-id="844c9-119">You can add a condition so that your logic app sends email only when hello new post belongs tooa specific category.</span></span>

1. <span data-ttu-id="844c9-120">Hola [portal de Azure](https://portal.azure.com), busque y abra la aplicación lógica en el Diseñador de la lógica de aplicación.</span><span class="sxs-lookup"><span data-stu-id="844c9-120">In hello [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="844c9-121">Agregar una ubicación de flujo de trabajo de toohello de condición que desea.</span><span class="sxs-lookup"><span data-stu-id="844c9-121">Add a condition toohello workflow location that you want.</span></span> 

   <span data-ttu-id="844c9-122">condición de hello tooadd entre los pasos existentes en el flujo de trabajo de aplicación de lógica de hello, Mover puntero de hello sobre flecha Hola donde desea que la condición de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="844c9-122">tooadd hello condition between existing steps in hello logic app workflow, move hello pointer over hello arrow where you want tooadd hello condition.</span></span> 
   <span data-ttu-id="844c9-123">Elija hello **signo** (**+**), a continuación, elija **agregar una condición**.</span><span class="sxs-lookup"><span data-stu-id="844c9-123">Choose hello **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="844c9-124">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="844c9-124">For example:</span></span>

   ![Agregar condición toologic aplicación](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="844c9-126">Si desea tooadd una condición de final de hello del flujo de trabajo actual, vaya toohello inferior de la aplicación lógica y elija **+ nuevo paso**.</span><span class="sxs-lookup"><span data-stu-id="844c9-126">If you want tooadd a condition at hello end of your current workflow, go toohello bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="844c9-127">Definir condición de Hola.</span><span class="sxs-lookup"><span data-stu-id="844c9-127">Now define hello condition.</span></span> <span data-ttu-id="844c9-128">Especificar el campo de origen de Hola que desea tooevaluate, Hola operación tooperform y el valor del objetivo de Hola o campo.</span><span class="sxs-lookup"><span data-stu-id="844c9-128">Specify hello source field that you want tooevaluate, hello operation tooperform, and hello target value or field.</span></span> <span data-ttu-id="844c9-129">tooadd existente campos condición tooyour, elegir hello **agregar lista de contenido dinámico**.</span><span class="sxs-lookup"><span data-stu-id="844c9-129">tooadd existing fields tooyour condition, choose from hello **Add dynamic content list**.</span></span>

   <span data-ttu-id="844c9-130">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="844c9-130">For example:</span></span>

   ![Edición de una condición en modo básico](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="844c9-132">Esta es la condición completa hello:</span><span class="sxs-lookup"><span data-stu-id="844c9-132">Here's hello complete condition:</span></span>

   ![Condición completa](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="844c9-134">condición de hello toodefine en el código, elija **editar en el modo avanzado**.</span><span class="sxs-lookup"><span data-stu-id="844c9-134">toodefine hello condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="844c9-135">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="844c9-135">For example:</span></span>
   > 
   > ![Edición de la condición en el código](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="844c9-137">En **Sí si** y **si NO**, agregar Hola pasos tooperform en función de si se cumple la condición de Hola.</span><span class="sxs-lookup"><span data-stu-id="844c9-137">Under **IF YES** and **IF NO**, add hello steps tooperform based on whether hello condition is met.</span></span>

   <span data-ttu-id="844c9-138">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="844c9-138">For example:</span></span>

   ![Condición con las trayectoria en caso de AFIRMATIVO y NEGATIVO](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="844c9-140">Puede arrastrar acciones existentes en hello **Sí si** y **si NO** las rutas de acceso.</span><span class="sxs-lookup"><span data-stu-id="844c9-140">You can drag existing actions into hello **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="844c9-141">Cuando haya terminado, guarde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="844c9-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="844c9-142">Ahora obtendrá los correos electrónicos sólo cuando Hola entradas cumplen la condición.</span><span class="sxs-lookup"><span data-stu-id="844c9-142">Now you get emails only when hello posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="844c9-143">Repetición de acciones de una lista con forEach</span><span class="sxs-lookup"><span data-stu-id="844c9-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="844c9-144">bucle forEach de Hello especifica un toorepeat de matriz una acción sobre él.</span><span class="sxs-lookup"><span data-stu-id="844c9-144">hello forEach loop specifies an array toorepeat an action over.</span></span> <span data-ttu-id="844c9-145">Si no es una matriz, se produce un error en el flujo de Hola.</span><span class="sxs-lookup"><span data-stu-id="844c9-145">If it is not an array, hello flow fails.</span></span> <span data-ttu-id="844c9-146">Por ejemplo, si tiene action1 que genera una matriz de mensajes y desea toosend cada mensaje, puede incluir esta instrucción forEach en Propiedades de saludo de la acción:`forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="844c9-146">For example, if you have action1 that outputs an array of messages, and you want toosend each message, you can include this forEach statement in hello properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-hello-code-definition-for-a-logic-app"></a><span data-ttu-id="844c9-147">Editar definición de código de hello para una aplicación de lógica</span><span class="sxs-lookup"><span data-stu-id="844c9-147">Edit hello code definition for a logic app</span></span>

<span data-ttu-id="844c9-148">Aunque tienen Hola diseñador la lógica de aplicación, puede editar directamente el código de hello que define una aplicación de la lógica.</span><span class="sxs-lookup"><span data-stu-id="844c9-148">Although you have hello Logic App Designer, you can directly edit hello code that defines a logic app.</span></span>

1. <span data-ttu-id="844c9-149">En la barra de comandos de hello, elija **vista código**.</span><span class="sxs-lookup"><span data-stu-id="844c9-149">On hello command bar, choose **Code view**.</span></span>

    <span data-ttu-id="844c9-150">Un completo editor abre y muestra la definición de hello editó.</span><span class="sxs-lookup"><span data-stu-id="844c9-150">A full editor opens and shows hello definition you edited.</span></span>

    ![vista Código](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="844c9-152">En el editor de texto hello, puede copiar y pegar cualquier número de las acciones de hello misma lógica de aplicación o entre aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="844c9-152">In hello text editor, you can copy and paste any number of actions within hello same logic app or between logic apps.</span></span> 
    <span data-ttu-id="844c9-153">Puede agregar o quitar secciones completas de definición de hello también fácilmente, y también pueden compartir las definiciones con otros.</span><span class="sxs-lookup"><span data-stu-id="844c9-153">You can also easily add or remove entire sections from hello definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="844c9-154">las modificaciones, elija a toosave **guardar**.</span><span class="sxs-lookup"><span data-stu-id="844c9-154">toosave your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="844c9-155">parameters</span><span class="sxs-lookup"><span data-stu-id="844c9-155">Parameters</span></span>

<span data-ttu-id="844c9-156">Algunas funcionalidades de Logic Apps solo están disponibles en la vista de código, como, por ejemplo, los parámetros.</span><span class="sxs-lookup"><span data-stu-id="844c9-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="844c9-157">Parámetros que sea fácil tooreuse valores a lo largo de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="844c9-157">Parameters make it easy tooreuse values throughout your logic app.</span></span> <span data-ttu-id="844c9-158">Por ejemplo, si tiene una dirección de correo electrónico que desea utilizar en varias acciones, debe definirla como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="844c9-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="844c9-159">Parámetros son buenos para extraer los valores que son muy toochange probable.</span><span class="sxs-lookup"><span data-stu-id="844c9-159">Parameters are good for pulling out values that you are likely toochange a lot.</span></span> <span data-ttu-id="844c9-160">Son especialmente útiles cuando necesite toooverride parámetros en entornos diferentes.</span><span class="sxs-lookup"><span data-stu-id="844c9-160">They are especially useful when you need toooverride parameters in different environments.</span></span> <span data-ttu-id="844c9-161">toolearn toooverride los parámetros basados en el entorno, vea [crear definiciones de aplicación lógica](../logic-apps/logic-apps-author-definitions.md) y [documentación de la API de REST](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="844c9-161">toolearn how toooverride parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="844c9-162">Este ejemplo se muestra cómo tooupdate la aplicación lógica existente para que puedan utilizar parámetros de término de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="844c9-162">This example shows how tooupdate your existing logic app so that you can use parameters for hello query term.</span></span>

1. <span data-ttu-id="844c9-163">En la vista de código, busque hello `parameters : {}` objeto y agregar un `currentFeedUrl` objeto:</span><span class="sxs-lookup"><span data-stu-id="844c9-163">In code view, find hello `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="844c9-164">Vaya toohello `When_a_feed-item_is_published` acción, buscar hello `queries` sección y reemplace el valor de la consulta de hello con:`"feedUrl": "#@{parameters('currentFeedUrl')}"`</span><span class="sxs-lookup"><span data-stu-id="844c9-164">Go toohello `When_a_feed-item_is_published` action, find hello `queries` section, and replace hello query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="844c9-165">toojoin dos o más cadenas, también puede usar hello `concat` función.</span><span class="sxs-lookup"><span data-stu-id="844c9-165">toojoin two or more strings, you can also use hello `concat` function.</span></span> 
    <span data-ttu-id="844c9-166">Por ejemplo, `"@concat('#',parameters('currentFeedUrl'))"` funciona igual Hola como Hola anterior.</span><span class="sxs-lookup"><span data-stu-id="844c9-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works hello same as hello above.</span></span>

3.  <span data-ttu-id="844c9-167">Cuando termine, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="844c9-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="844c9-168">Ahora puede cambiar fuente pasando una dirección URL diferente a través de Hola RSS del sitio Web de hello `currentFeedURL` objeto.</span><span class="sxs-lookup"><span data-stu-id="844c9-168">Now you can change hello website's RSS feed by passing a different URL through hello `currentFeedURL` object.</span></span>

<span data-ttu-id="844c9-169">Obtenga más información sobre [cómo definiciones de aplicación lógica de tooauthor](../logic-apps/logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="844c9-169">Learn more about [how tooauthor logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="844c9-170">Inicio de flujos de trabajo de aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="844c9-170">Start logic app workflows</span></span>

<span data-ttu-id="844c9-171">Tener distintas opciones para iniciar el flujo de trabajo de hello definido en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="844c9-171">You have different options for starting hello workflow defined in your logic app.</span></span> <span data-ttu-id="844c9-172">Siempre puede iniciar un flujo de trabajo a petición en hello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="844c9-172">You can always start a workflow on-demand in hello [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="844c9-173">Desencadenadores periódicos</span><span class="sxs-lookup"><span data-stu-id="844c9-173">Recurrence triggers</span></span>

<span data-ttu-id="844c9-174">Un desencadenador periódico se ejecuta en un intervalo que especifique.</span><span class="sxs-lookup"><span data-stu-id="844c9-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="844c9-175">Cuando el desencadenador de hello tiene lógica condicional, desencadenador Hola determina si el flujo de trabajo de hello debe toorun.</span><span class="sxs-lookup"><span data-stu-id="844c9-175">When hello trigger has conditional logic, hello trigger determines whether hello workflow needs toorun.</span></span> <span data-ttu-id="844c9-176">Un desencadenador indica que debe ejecutar el flujo de trabajo de hello devolviendo un `200` código de estado.</span><span class="sxs-lookup"><span data-stu-id="844c9-176">A trigger indicates hello workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="844c9-177">Flujo de trabajo de hello necesita toorun, desencadenador de hello devuelve un `202` código de estado.</span><span class="sxs-lookup"><span data-stu-id="844c9-177">When hello workflow doesn't need toorun, hello trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="844c9-178">Devolución de llamada mediante las API de REST</span><span class="sxs-lookup"><span data-stu-id="844c9-178">Callback using REST APIs</span></span>

<span data-ttu-id="844c9-179">toostart un flujo de trabajo, servicios pueden llamar a un punto de conexión de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="844c9-179">toostart a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="844c9-180">Este tipo de lógica aplicación a petición, elija a toostart **ejecutar ahora** en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="844c9-180">toostart this kind of logic app on-demand, choose **Run now** on hello command bar.</span></span> <span data-ttu-id="844c9-181">Vea [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md) (Inicio de flujos de trabajo mediante llamadas a puntos de conexión de aplicación lógica como desencadenadores).</span><span class="sxs-lookup"><span data-stu-id="844c9-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
[portal de Azure]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="844c9-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="844c9-183">Next steps</span></span>

* [<span data-ttu-id="844c9-184">Instrucciones switch</span><span class="sxs-lookup"><span data-stu-id="844c9-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="844c9-185">Bucles, ámbitos y desagrupación</span><span class="sxs-lookup"><span data-stu-id="844c9-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="844c9-186">Creación de definiciones de aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="844c9-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)