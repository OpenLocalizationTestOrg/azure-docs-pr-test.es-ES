---
title: mensajes EDIFACT aaaDecode - Azure Logic Apps | Documentos de Microsoft
description: "Validar EDI y generar confirmaciones con descodificador de mensaje de saludo EDIFACT Hola paquete de integración empresarial para las aplicaciones lógicas de Azure"
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
ms.openlocfilehash: 94faebdec4e4ffc8ad76ad1609495ddf9f002250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="cf983-103">Descodificar mensajes EDIFACT para las aplicaciones lógicas de Azure con hello paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="cf983-103">Decode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="cf983-104">Con el conector de mensaje de Hola descodificar EDIFACT, puede validar EDI y propiedades específicas del partner, dividir intercambios en conjuntos de transacciones o conservar todos intercambios y generar confirmaciones de transacciones procesadas.</span><span class="sxs-lookup"><span data-stu-id="cf983-104">With hello Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="cf983-105">toouse este conector, debe agregar Hola conector tooan existente desencadenador en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="cf983-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="cf983-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="cf983-106">Before you start</span></span>

<span data-ttu-id="cf983-107">Aquí es elementos de Hola que necesita:</span><span class="sxs-lookup"><span data-stu-id="cf983-107">Here's hello items you need:</span></span>

* <span data-ttu-id="cf983-108">Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="cf983-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="cf983-109">Una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md) que ya esté definida y asociada a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf983-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="cf983-110">Debe tener un conector de mensaje integración cuenta toouse Hola descodificar EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="cf983-110">You must have an integration account toouse hello Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="cf983-111">Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="cf983-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="cf983-112">Un [contrato EDIFACT](logic-apps-enterprise-integration-edifact.md) ya definido en la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="cf983-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="cf983-113">Descodificación de mensajes EDIFACT</span><span class="sxs-lookup"><span data-stu-id="cf983-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="cf983-114">[Creación de una aplicación lógica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="cf983-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="cf983-115">Conector de mensaje de Hola EDIFACT descodificar no tiene desencadenadores, por lo que debe agregar un desencadenador para iniciar la aplicación lógica, como un desencadenador de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="cf983-115">hello Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="cf983-116">Hola diseñador la lógica de aplicación, agregar un desencadenador y, a continuación, agregar una aplicación de lógica de tooyour de acción.</span><span class="sxs-lookup"><span data-stu-id="cf983-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3. <span data-ttu-id="cf983-117">En el cuadro de búsqueda de hello, escriba "EDIFACT" como filtro.</span><span class="sxs-lookup"><span data-stu-id="cf983-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="cf983-118">Seleccione **Descodificar mensaje EDIFACT**.</span><span class="sxs-lookup"><span data-stu-id="cf983-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![buscar EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="cf983-120">Si previamente no creó ninguna conexión de cuenta de integración de tooyour, se te pedirá toocreate ahora esa conexión.</span><span class="sxs-lookup"><span data-stu-id="cf983-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="cf983-121">Nombre de la conexión y seleccione cuenta de integración de Hola que desea tooconnect.</span><span class="sxs-lookup"><span data-stu-id="cf983-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![crear cuenta de integración](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="cf983-123">Aquellas propiedades con un asterisco son obligatorias.</span><span class="sxs-lookup"><span data-stu-id="cf983-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="cf983-124">Propiedad</span><span class="sxs-lookup"><span data-stu-id="cf983-124">Property</span></span> | <span data-ttu-id="cf983-125">Detalles</span><span class="sxs-lookup"><span data-stu-id="cf983-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="cf983-126">Nombre de la conexión *</span><span class="sxs-lookup"><span data-stu-id="cf983-126">Connection Name *</span></span> |<span data-ttu-id="cf983-127">Escriba cualquier nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="cf983-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="cf983-128">Cuenta de integración*</span><span class="sxs-lookup"><span data-stu-id="cf983-128">Integration Account *</span></span> |<span data-ttu-id="cf983-129">Escriba un nombre para la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="cf983-129">Enter a name for your integration account.</span></span> <span data-ttu-id="cf983-130">Asegúrese de que la aplicación de cuenta y la lógica de integración están en hello misma ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf983-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

4. <span data-ttu-id="cf983-131">Cuando haya terminado toofinish crear la conexión, elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="cf983-131">When you're done toofinish creating your connection, choose **Create**.</span></span> <span data-ttu-id="cf983-132">Los detalles de la conexión deben tener un aspecto similar ejemplo toothis:</span><span class="sxs-lookup"><span data-stu-id="cf983-132">Your connection details should look similar toothis example:</span></span>

    ![detalles de la cuenta de integración](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="cf983-134">Una vez creada la conexión, como se muestra en este ejemplo, seleccione toodecode de mensaje de archivo sin formato de EDIFACT Hola.</span><span class="sxs-lookup"><span data-stu-id="cf983-134">After your connection is created, as shown in this example, select hello EDIFACT flat file message toodecode.</span></span>

    ![creación de la conexión de la cuenta de integración](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="cf983-136">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cf983-136">For example:</span></span>

    ![Selección del mensaje de archivo plano EDIFACT para descodificar](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="cf983-138">Detalles de descodificador de EDIFACT</span><span class="sxs-lookup"><span data-stu-id="cf983-138">EDIFACT decoder details</span></span>

<span data-ttu-id="cf983-139">Hola descodificar EDIFACT conector lleva a cabo estas tareas:</span><span class="sxs-lookup"><span data-stu-id="cf983-139">hello Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="cf983-140">Valida el sobre de hello en el acuerdo de socio comercial.</span><span class="sxs-lookup"><span data-stu-id="cf983-140">Validates hello envelope against trading partner agreement.</span></span>
* <span data-ttu-id="cf983-141">Hola acuerdo se resuelve haciendo coincidir el calificador de remitente de hello & identificador y calificador de receptor & identificador.</span><span class="sxs-lookup"><span data-stu-id="cf983-141">Resolves hello agreement by matching hello sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="cf983-142">Divide un intercambio en varias transacciones al intercambio de hello tiene más de una transacción en función del contrato de hello opciones de configuración de recepción.</span><span class="sxs-lookup"><span data-stu-id="cf983-142">Splits an interchange into multiple transactions when hello interchange has more than one transaction based on hello agreement's receive settings configuration.</span></span>
* <span data-ttu-id="cf983-143">Desensambla el intercambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf983-143">Disassembles hello interchange.</span></span>
* <span data-ttu-id="cf983-144">Valida las propiedades de EDI y específicas del asociado, lo que incluye:</span><span class="sxs-lookup"><span data-stu-id="cf983-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="cf983-145">Validación de la estructura de envoltura de intercambio de Hola</span><span class="sxs-lookup"><span data-stu-id="cf983-145">Validation of hello interchange envelope structure</span></span>
  * <span data-ttu-id="cf983-146">Validación de esquemas de sobres de hello en el esquema de control hello</span><span class="sxs-lookup"><span data-stu-id="cf983-146">Schema validation of hello envelope against hello control schema</span></span>
  * <span data-ttu-id="cf983-147">Validación de esquema de los elementos de datos de conjuntos de transacciones de hello en el esquema de mensaje de Hola</span><span class="sxs-lookup"><span data-stu-id="cf983-147">Schema validation of hello transaction-set data elements against hello message schema</span></span>
  * <span data-ttu-id="cf983-148">Validación de EDI realizada en los elementos de datos del conjunto de transacciones</span><span class="sxs-lookup"><span data-stu-id="cf983-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="cf983-149">Comprueba que números de control de conjunto de intercambio, grupo y transacción hello no sean duplicados (si está configurado)</span><span class="sxs-lookup"><span data-stu-id="cf983-149">Verifies that hello interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="cf983-150">Comprueba el número de control de intercambio de hello en los intercambios recibidos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cf983-150">Checks hello interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="cf983-151">Comprueba el número de control de grupo de hello con los otros números de control de grupo en el intercambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf983-151">Checks hello group control number against other group control numbers in hello interchange.</span></span> 
  * <span data-ttu-id="cf983-152">Comprueba el número de control del conjunto de transacciones de hello en otros números de control de conjunto de transacciones de ese grupo.</span><span class="sxs-lookup"><span data-stu-id="cf983-152">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="cf983-153">Hola Intercambio en conjuntos de transacciones se divide o conserva todo el intercambio hello:</span><span class="sxs-lookup"><span data-stu-id="cf983-153">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="cf983-154">Divide el intercambio como conjuntos de transacciones (suspende conjuntos de transacciones en caso de error): divide el intercambio en conjuntos de transacciones y analiza cada conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="cf983-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="cf983-155">acción de descodificación de Hello X12 envía solo esos conjuntos de transacciones que no superan la validación demasiado`badMessages`y genera Hola transacciones restantes se establece demasiado`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="cf983-155">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="cf983-156">Divide el intercambio como conjuntos de transacciones (suspende el intercambio en caso de error): divide el intercambio en conjuntos de transacciones y analiza cada conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="cf983-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="cf983-157">Si una o más conjuntos de transacciones en la validación de un error de intercambio de hello, acción de descodificación de hello X12 genera conjuntos de todas las transacciones de hello en dicho intercambio demasiado`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="cf983-157">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="cf983-158">Conservar intercambio: suspender conjuntos de transacciones en caso de error: conservar intercambio de Hola y proceso Hola todo el intercambio por lotes.</span><span class="sxs-lookup"><span data-stu-id="cf983-158">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="cf983-159">acción de descodificación de Hello X12 envía solo esos conjuntos de transacciones que no superan la validación demasiado`badMessages`y genera Hola transacciones restantes se establece demasiado`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="cf983-159">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="cf983-160">Conservar intercambio: suspender intercambio en caso de error: conservar intercambio de Hola y proceso Hola todo el intercambio por lotes.</span><span class="sxs-lookup"><span data-stu-id="cf983-160">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="cf983-161">Si una o más conjuntos de transacciones en la validación de un error de intercambio de hello, acción de descodificación de hello X12 genera conjuntos de todas las transacciones de hello en dicho intercambio demasiado`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="cf983-161">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
* <span data-ttu-id="cf983-162">Genera una confirmación técnica (control) o funcional (si esta opción está configurada).</span><span class="sxs-lookup"><span data-stu-id="cf983-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="cf983-163">Una confirmación técnica o hello CONTRL ACK informa de los resultados de Hola de una comprobación sintáctica del intercambio de hello completo recibido.</span><span class="sxs-lookup"><span data-stu-id="cf983-163">A Technical Acknowledgment or hello CONTRL ACK reports hello results of a syntactical check of hello complete received interchange.</span></span>
  * <span data-ttu-id="cf983-164">Una confirmación funcional confirma la aceptación o el rechazo de un intercambio recibido o un grupo</span><span class="sxs-lookup"><span data-stu-id="cf983-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="cf983-165">Ver el archivo de Swagger</span><span class="sxs-lookup"><span data-stu-id="cf983-165">View Swagger file</span></span>
<span data-ttu-id="cf983-166">detalles de Swagger de tooview hello para el conector de saludo EDIFACT, vea [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="cf983-166">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf983-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf983-167">Next steps</span></span>
[<span data-ttu-id="cf983-168">Obtener más información sobre Hola paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="cf983-168">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial") 

