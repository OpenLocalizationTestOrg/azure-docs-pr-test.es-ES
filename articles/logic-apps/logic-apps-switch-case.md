---
title: "Uso de la instrucción switch para diferentes acciones en Azure Logic Apps | Microsoft Docs"
description: "Elija diferentes acciones para realizarlas en Logic Apps en función de los valores de expresión mediante una instrucción switch."
services: logic-apps
keywords: "Instrucción switch"
author: derek1ee
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: LADocs; deli
ms.openlocfilehash: 338b6a5b549d7bf81186550295608438ac4aee32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="67011-104">Diferentes acciones en Logic Apps con una instrucción switch</span><span class="sxs-lookup"><span data-stu-id="67011-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="67011-105">Al crear un flujo de trabajo, a menudo es necesario realizar diferentes acciones en función del valor de un objeto o una expresión.</span><span class="sxs-lookup"><span data-stu-id="67011-105">When authoring a workflow, you often have to take different actions based on the value of an object or expression.</span></span> <span data-ttu-id="67011-106">Por ejemplo, puede que desee que la aplicación lógica se comporte de manera diferente según el código de estado de una solicitud HTTP o una opción seleccionada en un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="67011-106">For example, you might want your logic app to behave differently based on the status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="67011-107">Puede utilizar una instrucción switch para implementar estos escenarios.</span><span class="sxs-lookup"><span data-stu-id="67011-107">You can use a switch statement to implement these scenarios.</span></span> <span data-ttu-id="67011-108">La aplicación lógica puede evaluar un token o una expresión y elegir el caso con el mismo valor para ejecutar las acciones especificadas.</span><span class="sxs-lookup"><span data-stu-id="67011-108">Your logic app can evaluate a token or expression, and choose the case with the same value to execute the specified actions.</span></span> <span data-ttu-id="67011-109">Solamente un caso debe cumplir la instrucción switch.</span><span class="sxs-lookup"><span data-stu-id="67011-109">Only one case should match the switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="67011-110">Al igual que todos los lenguajes de programación, la instrucción switch solo admite los operadores de igualdad.</span><span class="sxs-lookup"><span data-stu-id="67011-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="67011-111">Utilice una instrucción de condición si necesita otros operadores relacionales, como "mayor que".</span><span class="sxs-lookup"><span data-stu-id="67011-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="67011-112">Para garantizar el comportamiento de ejecución determinístico, los casos deben contener un valor único y estático en lugar de tokens dinámicos o una expresión.</span><span class="sxs-lookup"><span data-stu-id="67011-112">To ensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67011-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="67011-113">Prerequisites</span></span>

- <span data-ttu-id="67011-114">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="67011-114">An active Azure subscription.</span></span> <span data-ttu-id="67011-115">Si no tiene una suscripción de Azure activa, [cree una cuenta gratuita](https://azure.microsoft.com/free/) o pruebe [Logic Apps gratis](https://tryappservice.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="67011-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="67011-116">Conocimientos básicos acerca de Logic Apps</span><span class="sxs-lookup"><span data-stu-id="67011-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-to-your-workflow"></a><span data-ttu-id="67011-117">Adición de una instrucción switch al flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="67011-117">Add a switch statement to your workflow</span></span>

<span data-ttu-id="67011-118">Para mostrar cómo funciona una instrucción switch, este ejemplo crea una aplicación lógica que supervisa los archivos cargados en Dropbox.</span><span class="sxs-lookup"><span data-stu-id="67011-118">To show how a switch statement works, this example creates a logic app that monitors files uploaded to Dropbox.</span></span> <span data-ttu-id="67011-119">Cuando se cargan los nuevos archivos, la aplicación lógica envía un mensaje de correo electrónico a un aprobador que decide si se transfieren esos archivos a SharePoint.</span><span class="sxs-lookup"><span data-stu-id="67011-119">When the new files are uploaded, the logic app sends email to an approver who chooses whether to transfer those files to SharePoint.</span></span> <span data-ttu-id="67011-120">La aplicación utiliza una instrucción switch que lleva a cabo diferentes acciones en función del valor que selecciona el aprobador.</span><span class="sxs-lookup"><span data-stu-id="67011-120">The app uses a switch statement that performs different actions based on the value that the approver selects.</span></span>

1. <span data-ttu-id="67011-121">Cree una aplicación lógica y seleccione el desencadenador **Dropbox - Cuando se crea un archivo** (Dropbox - Cuando se crea un archivo).</span><span class="sxs-lookup"><span data-stu-id="67011-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![Uso del desencadenador Dropbox - Cuando se crea un archivo](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="67011-123">En el desencadenador, agregue la acción **Outlook.com - Enviar correo electrónico de aprobación**.</span><span class="sxs-lookup"><span data-stu-id="67011-123">Under the trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="67011-124">Logic Apps también admite escenarios de enviar un correo electrónico de aprobación desde una cuenta de Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="67011-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="67011-125">Si no tiene ninguna conexión existente, se le pedirá que cree una.</span><span class="sxs-lookup"><span data-stu-id="67011-125">If you don't have an existing connection, you're prompted to create one.</span></span>
   - <span data-ttu-id="67011-126">Rellene todos los campos obligatorios.</span><span class="sxs-lookup"><span data-stu-id="67011-126">Fill in the required fields.</span></span> <span data-ttu-id="67011-127">Por ejemplo, en **Para**, especifique la dirección de correo electrónico para enviar el correo electrónico del aprobador.</span><span class="sxs-lookup"><span data-stu-id="67011-127">For example, under **To**, specify the email address for sending the approver email.</span></span>
   - <span data-ttu-id="67011-128">En **Opciones de usuario**, escriba `Approve, Reject`.</span><span class="sxs-lookup"><span data-stu-id="67011-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![Configuración de la conexión](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="67011-130">Agregue una instrucción switch.</span><span class="sxs-lookup"><span data-stu-id="67011-130">Add a switch statement.</span></span>

   - <span data-ttu-id="67011-131">Seleccione **+ Nuevo paso** > **... Más** > **Agregar un caso de conmutador**.</span><span class="sxs-lookup"><span data-stu-id="67011-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="67011-132">Ahora queremos seleccionar la acción que se va a realizar en función de la salida `SelectedOptions` desde la acción *Enviar correo electrónico de aprobación*.</span><span class="sxs-lookup"><span data-stu-id="67011-132">Now we want to select the action to perform based on the `SelectedOptions` output from the *Send approval email* action.</span></span> 
   <span data-ttu-id="67011-133">Puede encontrar este campo en el selector **Agregar contenido dinámico**.</span><span class="sxs-lookup"><span data-stu-id="67011-133">You can find this field in the **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="67011-134">Use *caso 1* para controlar cuándo el aprobador selecciona `Approve`.</span><span class="sxs-lookup"><span data-stu-id="67011-134">Use *Case 1* to handle when the approver selects `Approve`.</span></span>
     - <span data-ttu-id="67011-135">Si se aprueba, copie el archivo original en SharePoint Online con la acción [**SharePoint Online - Crear archivo**](../connectors/connectors-create-api-sharepointonline.md).</span><span class="sxs-lookup"><span data-stu-id="67011-135">If approved, copy the original file to SharePoint Online with the [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="67011-136">Agregue otra acción dentro del caso para notificar a los usuarios que está disponible un nuevo archivo en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="67011-136">Add another action within the case to notify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="67011-137">Agregue otro caso para controlar cuándo el aprobador selecciona `Reject`.</span><span class="sxs-lookup"><span data-stu-id="67011-137">Add another case to handle when user selects `Reject`.</span></span>
     - <span data-ttu-id="67011-138">Si se rechaza, envíe un correo electrónico de notificación que informe a otros aprobadores de que el archivo se rechaza y que no es necesario realizar ninguna otra acción.</span><span class="sxs-lookup"><span data-stu-id="67011-138">If rejected, send a notification email informing other approvers that the file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="67011-139">`SelectedOptions`solo proporciona dos opciones, por lo que podemos dejar el caso **Predeterminado** vacío.</span><span class="sxs-lookup"><span data-stu-id="67011-139">`SelectedOptions` provides only two options, so we can leave the **Default** case empty.</span></span>

   ![Instrucción switch](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="67011-141">Una instrucción switch necesita al menos un caso además del caso predeterminado.</span><span class="sxs-lookup"><span data-stu-id="67011-141">A switch statement needs at least one case in addition to the default case.</span></span>

4. <span data-ttu-id="67011-142">Después de la instrucción switch, elimine el archivo original cargado en Dropbox agregando la acción **Dropbox - Delete file** (Dropbox - Eliminar archivo).</span><span class="sxs-lookup"><span data-stu-id="67011-142">After the switch statement, delete the original file uploaded to Dropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="67011-143">Guarde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="67011-143">Save your logic app.</span></span> <span data-ttu-id="67011-144">Pruebe la aplicación cargando archivos en Dropbox.</span><span class="sxs-lookup"><span data-stu-id="67011-144">Test your app by uploading a file to Dropbox.</span></span> <span data-ttu-id="67011-145">En breve recibirá un correo electrónico de aprobación.</span><span class="sxs-lookup"><span data-stu-id="67011-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="67011-146">Seleccione una opción y observe el comportamiento.</span><span class="sxs-lookup"><span data-stu-id="67011-146">Select an option, and observe the behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="67011-147">Consulte cómo [supervisar las aplicaciones lógicas](logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="67011-147">Check out how to [monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-the-code-behind-switch-statements"></a><span data-ttu-id="67011-148">Conocimiento del código detrás de las instrucciones switch</span><span class="sxs-lookup"><span data-stu-id="67011-148">Understand the code behind switch statements</span></span>

<span data-ttu-id="67011-149">Ahora que ha creado correctamente una aplicación de lógica mediante una instrucción switch, echemos un vistazo a la definición de código en la instrucción switch.</span><span class="sxs-lookup"><span data-stu-id="67011-149">Now that you successfully created a logic app using a switch statement, let's look at the code definition behind the switch statement.</span></span>

```json
"Switch": {
    "type": "Switch",
    "expression": "@body('Send_approval_email')?['SelectedOption']",
    "cases": {
        "Case 1" : {
            "case" : "Approved",
            "actions" : {}
        },
        "Case 2" : {
            "case" : "Rejected",
            "actions" : {}
        }
    },
    "default": {
        "actions": {}
    },
    "runAfter": {
        "Send_approval_email": [
            "Succeeded"
        ]
    }
}
```

* <span data-ttu-id="67011-150">`"Switch"` es el nombre de la instrucción switch; puede cambiar su nombre para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="67011-150">`"Switch"` is the name of the switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="67011-151">`"type": "Switch"` indica que la acción es una instrucción switch.</span><span class="sxs-lookup"><span data-stu-id="67011-151">`"type": "Switch"` indicates that the action is a switch statement.</span></span> 
* <span data-ttu-id="67011-152">`"expression"` es la opción seleccionada del aprobador en este ejemplo, y se evalúa con respecto a cada caso declarado más adelante en la definición.</span><span class="sxs-lookup"><span data-stu-id="67011-152">`"expression"` is the approver's selected option in this example and is evaluated against each case declared later in the definition.</span></span> 
* <span data-ttu-id="67011-153">`"cases"` puede contener cualquier número de casos.</span><span class="sxs-lookup"><span data-stu-id="67011-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="67011-154">Para cada caso, `"Case *"` es el nombre predeterminado del caso; puede cambiar su nombre para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="67011-154">For each case, `"Case *"` is the default name of the case, which you can rename for readability.</span></span> 
<span data-ttu-id="67011-155">`"case"` especifica la etiqueta del caso, que la expresión switch usa para la comparación, y debe ser un valor único y constante.</span><span class="sxs-lookup"><span data-stu-id="67011-155">`"case"` specifies the case label, which the switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="67011-156">Si ninguno de los casos coincide con la expresión switch, se ejecutan las acciones bajo `"default"`.</span><span class="sxs-lookup"><span data-stu-id="67011-156">If none of the cases match the switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="67011-157">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="67011-157">Get help</span></span>

<span data-ttu-id="67011-158">Para formular preguntas, o responderlas, y ver lo que hacen otros usuarios de Azure Logic Apps, visite el [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="67011-158">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="67011-159">Para ayudar a mejorar Azure Logic Apps y los conectores, vote o envíe ideas en el [sitio de comentarios de usuario de Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="67011-159">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="67011-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="67011-160">Next steps</span></span>

- <span data-ttu-id="67011-161">Aprenda cómo [agregar condiciones](logic-apps-use-logic-app-features.md).</span><span class="sxs-lookup"><span data-stu-id="67011-161">Learn how to [add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="67011-162">Aprenda sobre el [control de errores y las excepciones](logic-apps-exception-handling.md).</span><span class="sxs-lookup"><span data-stu-id="67011-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="67011-163">Conozca más [funcionalidades del lenguaje de flujo de trabajo](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="67011-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>