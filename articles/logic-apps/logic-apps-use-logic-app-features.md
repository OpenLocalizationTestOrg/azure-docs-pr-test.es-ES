---
title: "Incorporación de condiciones e inicio de flujos de trabajo: Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: e632c48ed31e82536db55a9c54438bece0c38fd4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="472aa-103">Uso de las características de aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="472aa-103">Use Logic Apps features</span></span>

<span data-ttu-id="472aa-104">En un [tema anterior](../logic-apps/logic-apps-create-a-logic-app.md), creó su primera aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="472aa-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="472aa-105">Para controlar el flujo de trabajo de la aplicación lógica, puede especificar distintas rutas de acceso para que la aplicación lógica se ejecute y determinar cómo se procesan los datos de matrices, colecciones y lotes.</span><span class="sxs-lookup"><span data-stu-id="472aa-105">To control your logic app's workflow, you can specify different paths for your logic app to run and how to process data in arrays, collections, and batches.</span></span> <span data-ttu-id="472aa-106">Puede incluir estos elementos en el flujo de trabajo de la aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="472aa-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="472aa-107">Las condiciones y las instrucciones [switch](../logic-apps/logic-apps-switch-case.md) permiten que la aplicación lógica ejecute distintas acciones en función de que se cumplan determinadas condiciones.</span><span class="sxs-lookup"><span data-stu-id="472aa-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="472aa-108">Los [bucles](../logic-apps/logic-apps-loops-and-scopes.md) permiten que la aplicación lógica ejecute pasos varias veces.</span><span class="sxs-lookup"><span data-stu-id="472aa-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="472aa-109">Por ejemplo, puede repetir acciones en una matriz si usa un bucle **For_each**.</span><span class="sxs-lookup"><span data-stu-id="472aa-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="472aa-110">También puede repetir acciones hasta que se cumpla una condición si usa un bucle **Until**.</span><span class="sxs-lookup"><span data-stu-id="472aa-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="472aa-111">Los [ámbitos](../logic-apps/logic-apps-loops-and-scopes.md) permiten agrupar una serie de acciones juntas, por ejemplo, para implementar el control de excepciones.</span><span class="sxs-lookup"><span data-stu-id="472aa-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, to implement exception handling.</span></span>

* <span data-ttu-id="472aa-112">La [desagrupación](../logic-apps/logic-apps-loops-and-scopes.md) permite que la aplicación lógica inicie flujos de trabajo independientes para elementos de una matriz si usa el comando **SplitOn**.</span><span class="sxs-lookup"><span data-stu-id="472aa-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use the **SplitOn** command.</span></span>

<span data-ttu-id="472aa-113">En este tema se presentan otros conceptos de creación de la aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="472aa-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="472aa-114">Vista de código para editar una aplicación lógica existente</span><span class="sxs-lookup"><span data-stu-id="472aa-114">Code view to edit an existing logic app</span></span>
* <span data-ttu-id="472aa-115">Opciones para iniciar un flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="472aa-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="472aa-116">Condiciones: ejecutan pasos solo después de que se cumpla una condición</span><span class="sxs-lookup"><span data-stu-id="472aa-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="472aa-117">Para que la aplicación lógica ejecute pasos solo cuando los datos cumplen determinados criterios, puede agregar una condición que compare los datos del flujo de trabajo con campos o valores concretos.</span><span class="sxs-lookup"><span data-stu-id="472aa-117">To have your logic app run steps only when data meets specific criteria, you can add a condition that compares data in the workflow against specific fields or values.</span></span>

<span data-ttu-id="472aa-118">Por ejemplo, suponga que tiene una aplicación lógica que le envía demasiados correos electrónicos para entradas en la fuente RSS de un sitio web.</span><span class="sxs-lookup"><span data-stu-id="472aa-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="472aa-119">Puede agregar una condición para que la aplicación lógica solo envíe un correo electrónico cuando la nueva entrada pertenezca a una categoría específica.</span><span class="sxs-lookup"><span data-stu-id="472aa-119">You can add a condition so that your logic app sends email only when the new post belongs to a specific category.</span></span>

1. <span data-ttu-id="472aa-120">En [Azure Portal](https://portal.azure.com), busque y abra la aplicación lógica en el Diseñador de aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="472aa-120">In the [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="472aa-121">Agregue una condición a la ubicación del flujo de trabajo que quiera.</span><span class="sxs-lookup"><span data-stu-id="472aa-121">Add a condition to the workflow location that you want.</span></span> 

   <span data-ttu-id="472aa-122">Para agregar la condición entre pasos existentes en el flujo de trabajo de la aplicación lógica, mueva el puntero sobre la flecha en la que quiere agregar la condición.</span><span class="sxs-lookup"><span data-stu-id="472aa-122">To add the condition between existing steps in the logic app workflow, move the pointer over the arrow where you want to add the condition.</span></span> 
   <span data-ttu-id="472aa-123">Elija el **signo más** (**+**) y luego seleccione **Agregar una condición**.</span><span class="sxs-lookup"><span data-stu-id="472aa-123">Choose the **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="472aa-124">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="472aa-124">For example:</span></span>

   ![Incorporación de una condición a la aplicación lógica](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="472aa-126">Si quiere agregar una condición al final del flujo de trabajo actual, vaya a la parte inferior de la aplicación lógica y elija **+ Nuevo paso**.</span><span class="sxs-lookup"><span data-stu-id="472aa-126">If you want to add a condition at the end of your current workflow, go to the bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="472aa-127">Defina la condición.</span><span class="sxs-lookup"><span data-stu-id="472aa-127">Now define the condition.</span></span> <span data-ttu-id="472aa-128">Especifique el campo de origen que quiere evaluar, la operación que va a realizar y el valor o campo de destino.</span><span class="sxs-lookup"><span data-stu-id="472aa-128">Specify the source field that you want to evaluate, the operation to perform, and the target value or field.</span></span> <span data-ttu-id="472aa-129">Para agregar campos existentes, elija en la lista **Agregar contenido dinámico**.</span><span class="sxs-lookup"><span data-stu-id="472aa-129">To add existing fields to your condition, choose from the **Add dynamic content list**.</span></span>

   <span data-ttu-id="472aa-130">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="472aa-130">For example:</span></span>

   ![Edición de una condición en modo básico](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="472aa-132">Esta es la condición completa:</span><span class="sxs-lookup"><span data-stu-id="472aa-132">Here's the complete condition:</span></span>

   ![Condición completa](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="472aa-134">Para definir la condición en el código, elija **Editar en modo avanzado**.</span><span class="sxs-lookup"><span data-stu-id="472aa-134">To define the condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="472aa-135">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="472aa-135">For example:</span></span>
   > 
   > ![Edición de la condición en el código](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="472aa-137">En **EN CASO AFIRMATIVO** y **EN CASO NEGATIVO**, agregue los pasos que se van a realizar en función de que la condición se cumpla.</span><span class="sxs-lookup"><span data-stu-id="472aa-137">Under **IF YES** and **IF NO**, add the steps to perform based on whether the condition is met.</span></span>

   <span data-ttu-id="472aa-138">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="472aa-138">For example:</span></span>

   ![Condición con las trayectoria en caso de AFIRMATIVO y NEGATIVO](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="472aa-140">Puede arrastrar acciones existentes a las trayectorias **EN CASO AFIRMATIVO** y **EN CASO NEGATIVO**.</span><span class="sxs-lookup"><span data-stu-id="472aa-140">You can drag existing actions into the **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="472aa-141">Cuando haya terminado, guarde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="472aa-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="472aa-142">Ahora solo recibirá correos electrónicos cuando las entradas cumplan la condición.</span><span class="sxs-lookup"><span data-stu-id="472aa-142">Now you get emails only when the posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="472aa-143">Repetición de acciones de una lista con forEach</span><span class="sxs-lookup"><span data-stu-id="472aa-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="472aa-144">El bucle forEach especifica una matriz para repetir una acción varias veces.</span><span class="sxs-lookup"><span data-stu-id="472aa-144">The forEach loop specifies an array to repeat an action over.</span></span> <span data-ttu-id="472aa-145">Si no es una matriz se produce un error en el flujo.</span><span class="sxs-lookup"><span data-stu-id="472aa-145">If it is not an array, the flow fails.</span></span> <span data-ttu-id="472aa-146">Por ejemplo, si tiene action1, que genera una matriz de mensajes, y desea enviar cada mensaje, puede incluir esta instrucción forEach en las propiedades de la acción: `forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="472aa-146">For example, if you have action1 that outputs an array of messages, and you want to send each message, you can include this forEach statement in the properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-the-code-definition-for-a-logic-app"></a><span data-ttu-id="472aa-147">Edición de la definición de código para una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="472aa-147">Edit the code definition for a logic app</span></span>

<span data-ttu-id="472aa-148">Aunque cuenta con el Diseñador de aplicación lógica, puede editar directamente el código que define una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="472aa-148">Although you have the Logic App Designer, you can directly edit the code that defines a logic app.</span></span>

1. <span data-ttu-id="472aa-149">En la barra de comandos, haga clic en **Vista Código**.</span><span class="sxs-lookup"><span data-stu-id="472aa-149">On the command bar, choose **Code view**.</span></span>

    <span data-ttu-id="472aa-150">Se abre un editor completo que muestra la definición que ha modificado.</span><span class="sxs-lookup"><span data-stu-id="472aa-150">A full editor opens and shows the definition you edited.</span></span>

    ![vista Código](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="472aa-152">En el editor de texto, puede copiar y pegar cualquier cantidad de acciones dentro de la misma aplicación lógica o entre aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="472aa-152">In the text editor, you can copy and paste any number of actions within the same logic app or between logic apps.</span></span> 
    <span data-ttu-id="472aa-153">También puede agregar o quitar secciones completas de la definición, así como compartir definiciones con otros.</span><span class="sxs-lookup"><span data-stu-id="472aa-153">You can also easily add or remove entire sections from the definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="472aa-154">Para guardar los cambios, elija **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="472aa-154">To save your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="472aa-155">Parámetros</span><span class="sxs-lookup"><span data-stu-id="472aa-155">Parameters</span></span>

<span data-ttu-id="472aa-156">Algunas funcionalidades de Logic Apps solo están disponibles en la vista de código, como, por ejemplo, los parámetros.</span><span class="sxs-lookup"><span data-stu-id="472aa-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="472aa-157">Los parámetros facilitan volver a usar los valores en toda la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="472aa-157">Parameters make it easy to reuse values throughout your logic app.</span></span> <span data-ttu-id="472aa-158">Por ejemplo, si tiene una dirección de correo electrónico que desea utilizar en varias acciones, debe definirla como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="472aa-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="472aa-159">Los parámetros son una buena forma de extraer valores que probablemente cambie mucho.</span><span class="sxs-lookup"><span data-stu-id="472aa-159">Parameters are good for pulling out values that you are likely to change a lot.</span></span> <span data-ttu-id="472aa-160">Son especialmente útiles cuando necesite reemplazar parámetros en entornos diferentes.</span><span class="sxs-lookup"><span data-stu-id="472aa-160">They are especially useful when you need to override parameters in different environments.</span></span> <span data-ttu-id="472aa-161">Para obtener información sobre cómo invalidar los parámetros basados en el entorno, vea [Creación de definiciones de aplicación lógica](../logic-apps/logic-apps-author-definitions.md) y [Documentación de la API de REST](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="472aa-161">To learn how to override parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="472aa-162">En este ejemplo se muestra cómo actualizar la aplicación lógica existente, para que pueda usar los parámetros para el término de consulta.</span><span class="sxs-lookup"><span data-stu-id="472aa-162">This example shows how to update your existing logic app so that you can use parameters for the query term.</span></span>

1. <span data-ttu-id="472aa-163">En la vista de código, busque el objeto `parameters : {}` y agregue un objeto `currentFeedUrl`:</span><span class="sxs-lookup"><span data-stu-id="472aa-163">In code view, find the `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="472aa-164">Vaya a la acción `When_a_feed-item_is_published`, busque la sección `queries` y reemplace el valor de consulta por: `"feedUrl": "#@{parameters('currentFeedUrl')}"`.</span><span class="sxs-lookup"><span data-stu-id="472aa-164">Go to the `When_a_feed-item_is_published` action, find the `queries` section, and replace the query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="472aa-165">Para combinar dos o más cadenas, también puede usar la función `concat`.</span><span class="sxs-lookup"><span data-stu-id="472aa-165">To join two or more strings, you can also use the `concat` function.</span></span> 
    <span data-ttu-id="472aa-166">Por ejemplo, `"@concat('#',parameters('currentFeedUrl'))"` funciona igual que el anterior.</span><span class="sxs-lookup"><span data-stu-id="472aa-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works the same as the above.</span></span>

3.  <span data-ttu-id="472aa-167">Cuando termine, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="472aa-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="472aa-168">Ahora puede cambiar la fuente RSS del sitio web pasando una dirección URL diferente a través del objeto `currentFeedURL`.</span><span class="sxs-lookup"><span data-stu-id="472aa-168">Now you can change the website's RSS feed by passing a different URL through the `currentFeedURL` object.</span></span>

<span data-ttu-id="472aa-169">Obtenga más información sobre la [creación de definiciones de aplicación lógica](../logic-apps/logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="472aa-169">Learn more about [how to author logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="472aa-170">Inicio de flujos de trabajo de aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="472aa-170">Start logic app workflows</span></span>

<span data-ttu-id="472aa-171">Hay diferentes opciones para iniciar el flujo de trabajo definido en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="472aa-171">You have different options for starting the workflow defined in your logic app.</span></span> <span data-ttu-id="472aa-172">Un flujo de trabajo siempre se puede iniciar a petición en [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="472aa-172">You can always start a workflow on-demand in the [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="472aa-173">Desencadenadores periódicos</span><span class="sxs-lookup"><span data-stu-id="472aa-173">Recurrence triggers</span></span>

<span data-ttu-id="472aa-174">Un desencadenador periódico se ejecuta en un intervalo que especifique.</span><span class="sxs-lookup"><span data-stu-id="472aa-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="472aa-175">Cuando el desencadenador tiene lógica condicional, este determina si necesita ejecutar el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="472aa-175">When the trigger has conditional logic, the trigger determines whether the workflow needs to run.</span></span> <span data-ttu-id="472aa-176">Un desencadenador indica si se debe ejecutar el flujo de trabajo, para lo que devuelve un código de estado `200`.</span><span class="sxs-lookup"><span data-stu-id="472aa-176">A trigger indicates the workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="472aa-177">Cuando no es necesario ejecutar el flujo de trabajo, el desencadenador devuelve un código de estado `202`.</span><span class="sxs-lookup"><span data-stu-id="472aa-177">When the workflow doesn't need to run, the trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="472aa-178">Devolución de llamada mediante las API de REST</span><span class="sxs-lookup"><span data-stu-id="472aa-178">Callback using REST APIs</span></span>

<span data-ttu-id="472aa-179">Para iniciar un flujo de trabajo, los servicios pueden llamar a un punto de conexión de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="472aa-179">To start a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="472aa-180">Para iniciar ese tipo de aplicación lógica a petición, seleccione **Ejecutar ahora** en la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="472aa-180">To start this kind of logic app on-demand, choose **Run now** on the command bar.</span></span> <span data-ttu-id="472aa-181">Vea [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md) (Inicio de flujos de trabajo mediante llamadas a puntos de conexión de aplicación lógica como desencadenadores).</span><span class="sxs-lookup"><span data-stu-id="472aa-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
<span data-ttu-id="472aa-182">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="472aa-182">[Azure portal]: https://portal.azure.com</span></span>

## <a name="next-steps"></a><span data-ttu-id="472aa-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="472aa-183">Next steps</span></span>

* [<span data-ttu-id="472aa-184">Instrucciones switch</span><span class="sxs-lookup"><span data-stu-id="472aa-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="472aa-185">Bucles, ámbitos y desagrupación</span><span class="sxs-lookup"><span data-stu-id="472aa-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="472aa-186">Creación de definiciones de aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="472aa-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)