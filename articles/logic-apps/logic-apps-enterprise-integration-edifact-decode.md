---
title: "Descodificación de mensajes EDIFACT: Azure Logic Apps | Microsoft Docs"
description: Valide EDI y genere confirmaciones con el descodificador de mensajes EDIFACT en Enterprise Integration Pack para Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e3787b48037360bf6066ddce2bacba6842213b2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="a0e5e-103">Descodificación de mensajes EDIFACT para Azure Logic Apps con Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="a0e5e-103">Decode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="a0e5e-104">Con el conector de descodificación de mensajes EDIFACT, puede validar propiedades EDI y específicas de asociados, dividir intercambios en transacciones o conservar intercambios completos y originar la confirmación de las transacciones procesadas.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-104">With the Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="a0e5e-105">Para usar este conector, debe agregarlo a un desencadenador existente en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="a0e5e-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="a0e5e-106">Before you start</span></span>

<span data-ttu-id="a0e5e-107">Esto es lo que necesita:</span><span class="sxs-lookup"><span data-stu-id="a0e5e-107">Here's the items you need:</span></span>

* <span data-ttu-id="a0e5e-108">Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="a0e5e-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="a0e5e-109">Una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md) que ya esté definida y asociada a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="a0e5e-110">Debe tener una cuenta de integración para usar el conector de descodificación de mensajes EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-110">You must have an integration account to use the Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="a0e5e-111">Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="a0e5e-112">Un [contrato EDIFACT](logic-apps-enterprise-integration-edifact.md) ya definido en la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="a0e5e-113">Descodificación de mensajes EDIFACT</span><span class="sxs-lookup"><span data-stu-id="a0e5e-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="a0e5e-114">[Creación de una aplicación lógica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a0e5e-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="a0e5e-115">El conector de descodificación de mensajes EDIFACT no tiene desencadenadores, por lo que debe agregar uno para iniciar la aplicación lógica, por ejemplo, un desencadenador de solicitud.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-115">The Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="a0e5e-116">En el Diseñador de aplicaciones lógicas, agregue un desencadenador y una acción a la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3. <span data-ttu-id="a0e5e-117">En el cuadro de búsqueda, escriba "EDIFACT" para el filtro.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="a0e5e-118">Seleccione **Descodificar mensaje EDIFACT**.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![buscar EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="a0e5e-120">Si no había creado ninguna conexión a la cuenta de integración, se le pedirá que lo haga ahora.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="a0e5e-121">Asigne un nombre a la conexión y seleccione la cuenta de integración que desee conectar.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![crear cuenta de integración](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="a0e5e-123">Aquellas propiedades con un asterisco son obligatorias.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="a0e5e-124">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a0e5e-124">Property</span></span> | <span data-ttu-id="a0e5e-125">Detalles</span><span class="sxs-lookup"><span data-stu-id="a0e5e-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="a0e5e-126">Nombre de la conexión *</span><span class="sxs-lookup"><span data-stu-id="a0e5e-126">Connection Name *</span></span> |<span data-ttu-id="a0e5e-127">Escriba cualquier nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="a0e5e-128">Cuenta de integración*</span><span class="sxs-lookup"><span data-stu-id="a0e5e-128">Integration Account *</span></span> |<span data-ttu-id="a0e5e-129">Escriba un nombre para la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-129">Enter a name for your integration account.</span></span> <span data-ttu-id="a0e5e-130">Asegúrese de que la cuenta de integración y la aplicación lógica se encuentren en la misma ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

4. <span data-ttu-id="a0e5e-131">Cuando haya acabado, para terminar de crear la conexión, elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-131">When you're done to finish creating your connection, choose **Create**.</span></span> <span data-ttu-id="a0e5e-132">Los detalles de la conexión deberían ser similares a los de este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a0e5e-132">Your connection details should look similar to this example:</span></span>

    ![detalles de la cuenta de integración](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="a0e5e-134">Una vez creada la conexión, como se muestra en este ejemplo, seleccione el mensaje de archivo plano EDIFACT que desee descodificar.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-134">After your connection is created, as shown in this example, select the EDIFACT flat file message to decode.</span></span>

    ![creación de la conexión de la cuenta de integración](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="a0e5e-136">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a0e5e-136">For example:</span></span>

    ![Selección del mensaje de archivo plano EDIFACT para descodificar](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="a0e5e-138">Detalles de descodificador de EDIFACT</span><span class="sxs-lookup"><span data-stu-id="a0e5e-138">EDIFACT decoder details</span></span>

<span data-ttu-id="a0e5e-139">El conector de descodificación EDIFACT lleva a cabo estas tareas:</span><span class="sxs-lookup"><span data-stu-id="a0e5e-139">The Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="a0e5e-140">Valida el sobre con el acuerdo entre socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-140">Validates the envelope against trading partner agreement.</span></span>
* <span data-ttu-id="a0e5e-141">Resuelve el acuerdo, para lo que hace coincidir el calificador e identificador del remitente con el calificador e identificador del receptor.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-141">Resolves the agreement by matching the sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="a0e5e-142">Divide un intercambio en varias transacciones cuando el intercambio tiene más de una transacción que se basa en la configuración de recepción del acuerdo.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-142">Splits an interchange into multiple transactions when the interchange has more than one transaction based on the agreement's receive settings configuration.</span></span>
* <span data-ttu-id="a0e5e-143">Desensambla el intercambio.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-143">Disassembles the interchange.</span></span>
* <span data-ttu-id="a0e5e-144">Valida las propiedades de EDI y específicas del asociado, lo que incluye:</span><span class="sxs-lookup"><span data-stu-id="a0e5e-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="a0e5e-145">Validación de la estructura del sobre de intercambio</span><span class="sxs-lookup"><span data-stu-id="a0e5e-145">Validation of the interchange envelope structure</span></span>
  * <span data-ttu-id="a0e5e-146">Validación del esquema del sobre con respecto al esquema de control</span><span class="sxs-lookup"><span data-stu-id="a0e5e-146">Schema validation of the envelope against the control schema</span></span>
  * <span data-ttu-id="a0e5e-147">Validación del esquema de los elementos de datos del conjunto de transacciones con respecto al esquema de mensaje</span><span class="sxs-lookup"><span data-stu-id="a0e5e-147">Schema validation of the transaction-set data elements against the message schema</span></span>
  * <span data-ttu-id="a0e5e-148">Validación de EDI realizada en los elementos de datos del conjunto de transacciones</span><span class="sxs-lookup"><span data-stu-id="a0e5e-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="a0e5e-149">Comprueba que los números de control de intercambio, grupo y conjunto de transacciones no están duplicados (si está configurado).</span><span class="sxs-lookup"><span data-stu-id="a0e5e-149">Verifies that the interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="a0e5e-150">Comprueba el número de control del intercambio con los intercambios recibidos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-150">Checks the interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="a0e5e-151">Comprueba el número de control del grupo en relación con otros números de control de grupo en el intercambio.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-151">Checks the group control number against other group control numbers in the interchange.</span></span> 
  * <span data-ttu-id="a0e5e-152">Comprueba el número de control del conjunto de transacciones con otros números de control del conjunto de transacciones de dicho grupo.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-152">Checks the transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="a0e5e-153">Divide el intercambio en conjuntos de transacciones o conserva todo el intercambio:</span><span class="sxs-lookup"><span data-stu-id="a0e5e-153">Splits the interchange into transaction sets, or preserves the entire interchange:</span></span>
  * <span data-ttu-id="a0e5e-154">Divide el intercambio como conjuntos de transacciones (suspende conjuntos de transacciones en caso de error): divide el intercambio en conjuntos de transacciones y analiza cada conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="a0e5e-155">La acción de descodificación X12 solo genera esos conjuntos de transacciones que no superan la validación para `badMessages` y los resultados de las transacciones restantes se establecen en `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-155">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="a0e5e-156">Divide el intercambio como conjuntos de transacciones (suspende el intercambio en caso de error): divide el intercambio en conjuntos de transacciones y analiza cada conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="a0e5e-157">Si uno o varios conjuntos de transacciones del intercambio no superan la validación, la acción de descodificación de X12 establece todos los conjuntos de transacciones del intercambio en `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-157">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
  * <span data-ttu-id="a0e5e-158">Conserva el intercambio (suspende conjuntos de transacciones en caso de error): conserva el intercambio y procesa todo el intercambio por lotes.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-158">Preserve Interchange - suspend transaction sets on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="a0e5e-159">La acción de descodificación X12 solo genera esos conjuntos de transacciones que no superan la validación para `badMessages` y los resultados de las transacciones restantes se establecen en `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-159">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="a0e5e-160">Conserva el intercambio (suspende el intercambio en caso de error): conserva el intercambio y procesa todo el intercambio por lotes.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-160">Preserve Interchange - suspend interchange on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="a0e5e-161">Si uno o varios conjuntos de transacciones del intercambio no superan la validación, la acción X12 Decode establece todos los conjuntos de transacciones del intercambio en `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-161">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
* <span data-ttu-id="a0e5e-162">Genera una confirmación técnica (control) o funcional (si esta opción está configurada).</span><span class="sxs-lookup"><span data-stu-id="a0e5e-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="a0e5e-163">Una confirmación técnica o ACK CONTRL informa de los resultados de una comprobación sintáctica de todo el intercambio recibido.</span><span class="sxs-lookup"><span data-stu-id="a0e5e-163">A Technical Acknowledgment or the CONTRL ACK reports the results of a syntactical check of the complete received interchange.</span></span>
  * <span data-ttu-id="a0e5e-164">Una confirmación funcional confirma la aceptación o el rechazo de un intercambio recibido o un grupo</span><span class="sxs-lookup"><span data-stu-id="a0e5e-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="a0e5e-165">Ver el archivo de Swagger</span><span class="sxs-lookup"><span data-stu-id="a0e5e-165">View Swagger file</span></span>
<span data-ttu-id="a0e5e-166">Para ver los detalles de Swagger para el conector EDIFACT, consulte [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="a0e5e-166">To view the Swagger details for the EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0e5e-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a0e5e-167">Next steps</span></span>
[<span data-ttu-id="a0e5e-168">Más información sobre Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="a0e5e-168">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Información sobre Enterprise Integration Pack") 

