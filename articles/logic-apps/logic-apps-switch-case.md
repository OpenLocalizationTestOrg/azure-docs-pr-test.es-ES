---
title: "instrucción aaaSwitch para distintas acciones en las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Elija tooperform acciones diferentes en las aplicaciones lógicas basadas en valores de expresión mediante una instrucción switch"
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
ms.openlocfilehash: 09ed7e4a752003aba157e9156bf4dc89ef86f5ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="baa7e-104">Diferentes acciones en Logic Apps con una instrucción switch</span><span class="sxs-lookup"><span data-stu-id="baa7e-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="baa7e-105">Al crear un flujo de trabajo, tendrá a menudo tootake diferentes acciones basadas en valor de Hola de un objeto o una expresión.</span><span class="sxs-lookup"><span data-stu-id="baa7e-105">When authoring a workflow, you often have tootake different actions based on hello value of an object or expression.</span></span> <span data-ttu-id="baa7e-106">Por ejemplo, es recomendable su toobehave de aplicación lógica diferente en función de código de estado de Hola de una solicitud HTTP, como una opción seleccionada en un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="baa7e-106">For example, you might want your logic app toobehave differently based on hello status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="baa7e-107">Puede usar un tooimplement de la instrucción switch en estos escenarios.</span><span class="sxs-lookup"><span data-stu-id="baa7e-107">You can use a switch statement tooimplement these scenarios.</span></span> <span data-ttu-id="baa7e-108">La aplicación lógica puede evaluar un símbolo (token) o una expresión y elegir el caso de Hola Hola Hola de tooexecute valor mismo acciones especificadas.</span><span class="sxs-lookup"><span data-stu-id="baa7e-108">Your logic app can evaluate a token or expression, and choose hello case with hello same value tooexecute hello specified actions.</span></span> <span data-ttu-id="baa7e-109">Un solo caso debe coincidir con la instrucción switch de Hola.</span><span class="sxs-lookup"><span data-stu-id="baa7e-109">Only one case should match hello switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="baa7e-110">Al igual que todos los lenguajes de programación, la instrucción switch solo admite los operadores de igualdad.</span><span class="sxs-lookup"><span data-stu-id="baa7e-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="baa7e-111">Utilice una instrucción de condición si necesita otros operadores relacionales, como "mayor que".</span><span class="sxs-lookup"><span data-stu-id="baa7e-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="baa7e-112">comportamiento de ejecución determinista tooensure, casos deben contener un valor único y estático en lugar de símbolos (tokens) dinámico o una expresión.</span><span class="sxs-lookup"><span data-stu-id="baa7e-112">tooensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="baa7e-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="baa7e-113">Prerequisites</span></span>

- <span data-ttu-id="baa7e-114">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="baa7e-114">An active Azure subscription.</span></span> <span data-ttu-id="baa7e-115">Si no tiene una suscripción de Azure activa, [cree una cuenta gratuita](https://azure.microsoft.com/free/) o pruebe [Logic Apps gratis](https://tryappservice.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="baa7e-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="baa7e-116">Conocimientos básicos acerca de Logic Apps</span><span class="sxs-lookup"><span data-stu-id="baa7e-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a><span data-ttu-id="baa7e-117">Agregar un flujo de trabajo de tooyour de instrucción switch</span><span class="sxs-lookup"><span data-stu-id="baa7e-117">Add a switch statement tooyour workflow</span></span>

<span data-ttu-id="baa7e-118">tooshow el funcionamiento de una instrucción switch, en este ejemplo se crea una aplicación de lógica que supervisa los archivos cargan tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="baa7e-118">tooshow how a switch statement works, this example creates a logic app that monitors files uploaded tooDropbox.</span></span> <span data-ttu-id="baa7e-119">Cuando se cargan los nuevos archivos de hello, aplicación de lógica de hello envía aprobador de tooan de correo electrónico que elige si tootransfer tooSharePoint de esos archivos.</span><span class="sxs-lookup"><span data-stu-id="baa7e-119">When hello new files are uploaded, hello logic app sends email tooan approver who chooses whether tootransfer those files tooSharePoint.</span></span> <span data-ttu-id="baa7e-120">aplicación Hello usa una instrucción switch que lleva a cabo diferentes acciones basadas en el valor de Hola que Hola selecciona aprobador.</span><span class="sxs-lookup"><span data-stu-id="baa7e-120">hello app uses a switch statement that performs different actions based on hello value that hello approver selects.</span></span>

1. <span data-ttu-id="baa7e-121">Cree una aplicación lógica y seleccione el desencadenador **Dropbox - Cuando se crea un archivo** (Dropbox - Cuando se crea un archivo).</span><span class="sxs-lookup"><span data-stu-id="baa7e-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![Uso del desencadenador Dropbox - Cuando se crea un archivo](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="baa7e-123">En el desencadenador de hello, agregue esta acción: **Outlook.com - enviar correo electrónico de aprobación**</span><span class="sxs-lookup"><span data-stu-id="baa7e-123">Under hello trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="baa7e-124">Logic Apps también admite escenarios de enviar un correo electrónico de aprobación desde una cuenta de Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="baa7e-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="baa7e-125">Si no tiene una conexión existente, se le pedirá toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="baa7e-125">If you don't have an existing connection, you're prompted toocreate one.</span></span>
   - <span data-ttu-id="baa7e-126">Rellene los campos de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="baa7e-126">Fill in hello required fields.</span></span> <span data-ttu-id="baa7e-127">Por ejemplo, en **a**, especifique la dirección de correo electrónico de hello para el envío de correo electrónico de aprobador Hola.</span><span class="sxs-lookup"><span data-stu-id="baa7e-127">For example, under **To**, specify hello email address for sending hello approver email.</span></span>
   - <span data-ttu-id="baa7e-128">En **Opciones de usuario**, escriba `Approve, Reject`.</span><span class="sxs-lookup"><span data-stu-id="baa7e-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![Configuración de la conexión](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="baa7e-130">Agregue una instrucción switch.</span><span class="sxs-lookup"><span data-stu-id="baa7e-130">Add a switch statement.</span></span>

   - <span data-ttu-id="baa7e-131">Seleccione **+ Nuevo paso** > **... Más** > **Agregar un caso de conmutador**.</span><span class="sxs-lookup"><span data-stu-id="baa7e-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="baa7e-132">Ahora queremos tooselect Hola acción tooperform en función de hello `SelectedOptions` de salida de hello *enviar correo electrónico de aprobación* acción.</span><span class="sxs-lookup"><span data-stu-id="baa7e-132">Now we want tooselect hello action tooperform based on hello `SelectedOptions` output from hello *Send approval email* action.</span></span> 
   <span data-ttu-id="baa7e-133">Este campo se encuentra en hello **agregar contenido dinámico** selector.</span><span class="sxs-lookup"><span data-stu-id="baa7e-133">You can find this field in hello **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="baa7e-134">Use *caso 1* toohandle cuando selecciona Aprobador hello `Approve`.</span><span class="sxs-lookup"><span data-stu-id="baa7e-134">Use *Case 1* toohandle when hello approver selects `Approve`.</span></span>
     - <span data-ttu-id="baa7e-135">Si se aprueba, copie Hola original archivo tooSharePoint en línea con hello [ **SharePoint Online - crear archivo** acción](../connectors/connectors-create-api-sharepointonline.md).</span><span class="sxs-lookup"><span data-stu-id="baa7e-135">If approved, copy hello original file tooSharePoint Online with hello [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="baa7e-136">Agregar otra acción los usuarios de mayúsculas toonotify Hola que está disponible en SharePoint un nuevo archivo.</span><span class="sxs-lookup"><span data-stu-id="baa7e-136">Add another action within hello case toonotify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="baa7e-137">Agregar otro toohandle mayúscula cuando el usuario selecciona `Reject`.</span><span class="sxs-lookup"><span data-stu-id="baa7e-137">Add another case toohandle when user selects `Reject`.</span></span>
     - <span data-ttu-id="baa7e-138">Si rechaza, envíe un correo electrónico de notificación que le informa de otros aprobadores que se rechazó el archivo de Hola y no es necesaria realizar ninguna otra acción.</span><span class="sxs-lookup"><span data-stu-id="baa7e-138">If rejected, send a notification email informing other approvers that hello file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="baa7e-139">`SelectedOptions`proporciona solo dos opciones, por lo que podemos dejar hello **predeterminado** caso vacía.</span><span class="sxs-lookup"><span data-stu-id="baa7e-139">`SelectedOptions` provides only two options, so we can leave hello **Default** case empty.</span></span>

   ![Instrucción switch](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="baa7e-141">Una instrucción switch tiene al menos un caso en caso de adición toohello predeterminado.</span><span class="sxs-lookup"><span data-stu-id="baa7e-141">A switch statement needs at least one case in addition toohello default case.</span></span>

4. <span data-ttu-id="baa7e-142">Después de la instrucción switch de hello, eliminar Hola original tooDropbox de archivo cargado mediante la adición de esta acción: **Dropbox - eliminar archivo**</span><span class="sxs-lookup"><span data-stu-id="baa7e-142">After hello switch statement, delete hello original file uploaded tooDropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="baa7e-143">Guarde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="baa7e-143">Save your logic app.</span></span> <span data-ttu-id="baa7e-144">Probar la aplicación mediante la carga de un archivo tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="baa7e-144">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="baa7e-145">En breve recibirá un correo electrónico de aprobación.</span><span class="sxs-lookup"><span data-stu-id="baa7e-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="baa7e-146">Seleccione una opción y observar el comportamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="baa7e-146">Select an option, and observe hello behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="baa7e-147">Consulte cómo demasiado[supervisar las aplicaciones lógicas](logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="baa7e-147">Check out how too[monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-hello-code-behind-switch-statements"></a><span data-ttu-id="baa7e-148">Comprender el código de hello detrás de las instrucciones switch</span><span class="sxs-lookup"><span data-stu-id="baa7e-148">Understand hello code behind switch statements</span></span>

<span data-ttu-id="baa7e-149">Ahora que ha creado correctamente una aplicación de lógica mediante una instrucción switch, echemos un vistazo a la definición de código de hello detrás de la instrucción switch de Hola.</span><span class="sxs-lookup"><span data-stu-id="baa7e-149">Now that you successfully created a logic app using a switch statement, let's look at hello code definition behind hello switch statement.</span></span>

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

* <span data-ttu-id="baa7e-150">`"Switch"`es el nombre de saludo de la instrucción switch de hello, que puede cambiar el nombre para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="baa7e-150">`"Switch"` is hello name of hello switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="baa7e-151">`"type": "Switch"`indica que la acción de hello es una instrucción switch.</span><span class="sxs-lookup"><span data-stu-id="baa7e-151">`"type": "Switch"` indicates that hello action is a switch statement.</span></span> 
* <span data-ttu-id="baa7e-152">`"expression"`es la opción seleccionada del aprobador hello en este ejemplo y se evalúa con respecto a cada caso declarado más adelante en la definición de Hola.</span><span class="sxs-lookup"><span data-stu-id="baa7e-152">`"expression"` is hello approver's selected option in this example and is evaluated against each case declared later in hello definition.</span></span> 
* <span data-ttu-id="baa7e-153">`"cases"` puede contener cualquier número de casos.</span><span class="sxs-lookup"><span data-stu-id="baa7e-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="baa7e-154">Para cada caso, `"Case *"` es nombre predeterminado de Hola de caso de hello, que puede cambiar el nombre para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="baa7e-154">For each case, `"Case *"` is hello default name of hello case, which you can rename for readability.</span></span> 
<span data-ttu-id="baa7e-155">`"case"`Especifica la etiqueta case hello, que usar expresiones de conmutador para la comparación de Hola y debe ser un valor único y constante.</span><span class="sxs-lookup"><span data-stu-id="baa7e-155">`"case"` specifies hello case label, which hello switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="baa7e-156">Si ninguno de los casos de hello coincide con la expresión switch hello, acciones en el `"default"` se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="baa7e-156">If none of hello cases match hello switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="baa7e-157">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="baa7e-157">Get help</span></span>

<span data-ttu-id="baa7e-158">tooask preguntas y responder a preguntas, consulte ¿Qué otros usuarios de aplicaciones de la lógica de Azure están realizando, visitan hello [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="baa7e-158">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="baa7e-159">toohelp mejorar las aplicaciones lógicas de Azure y conectores, votar sobre o enviar ideas en hello [sitio de comentarios de usuario de Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="baa7e-159">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="baa7e-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="baa7e-160">Next steps</span></span>

- <span data-ttu-id="baa7e-161">Obtenga información acerca de cómo demasiado[agregar condiciones](logic-apps-use-logic-app-features.md)</span><span class="sxs-lookup"><span data-stu-id="baa7e-161">Learn how too[add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="baa7e-162">Aprenda sobre el [control de errores y las excepciones](logic-apps-exception-handling.md).</span><span class="sxs-lookup"><span data-stu-id="baa7e-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="baa7e-163">Conozca más [funcionalidades del lenguaje de flujo de trabajo](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="baa7e-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>