---
title: mensajes de aaaDecode X12 - Azure Logic Apps | Documentos de Microsoft
description: "Validar EDI y generar confirmaciones con descodificador de mensaje de Hola X12 Hola paquete de integración empresarial para las aplicaciones lógicas de Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1ffececca1ff835b319b64c85f86c421395833c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="4a9cf-103">Descodificar X12 mensajes para las aplicaciones lógicas de Azure con hello paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="4a9cf-103">Decode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="4a9cf-104">Con el conector de mensaje de Hola Decode X12, puede validar sobres Hola contra un acuerdo entre socios comerciales, validar EDI y propiedades específicas del partner, dividir intercambios en conjuntos de transacciones o conservar todos intercambios y generar confirmaciones de transacciones procesadas.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-104">With hello Decode X12 message connector, you can validate hello envelope against a trading partner agreement, validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="4a9cf-105">toouse este conector, debe agregar Hola conector tooan existente desencadenador en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="4a9cf-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="4a9cf-106">Before you start</span></span>

<span data-ttu-id="4a9cf-107">Aquí es elementos de Hola que necesita:</span><span class="sxs-lookup"><span data-stu-id="4a9cf-107">Here's hello items you need:</span></span>

* <span data-ttu-id="4a9cf-108">Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="4a9cf-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="4a9cf-109">Una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md) que ya esté definida y asociada a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="4a9cf-110">Debe tener un conector integración cuenta toouse Hola Decode X12 mensaje.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-110">You must have an integration account toouse hello Decode X12 message connector.</span></span>
* <span data-ttu-id="4a9cf-111">Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="4a9cf-112">Un [contrato X12](logic-apps-enterprise-integration-x12.md) ya definido en su cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="4a9cf-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="decode-x12-messages"></a><span data-ttu-id="4a9cf-113">Descodificación de mensajes X12</span><span class="sxs-lookup"><span data-stu-id="4a9cf-113">Decode X12 messages</span></span>

1. <span data-ttu-id="4a9cf-114">[Creación de una aplicación lógica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4a9cf-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="4a9cf-115">Conector de mensaje de Hola Decode X12 no tiene desencadenadores, por lo que debe agregar un desencadenador para iniciar la aplicación lógica, como un desencadenador de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-115">hello Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="4a9cf-116">Hola diseñador la lógica de aplicación, agregar un desencadenador y, a continuación, agregar una aplicación de lógica de tooyour de acción.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="4a9cf-117">En el cuadro de búsqueda de hello, escriba "x12" para el filtro.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="4a9cf-118">Seleccione **X12 - Decode X12 message** (X12 – Descodificación de mensajes X12).</span><span class="sxs-lookup"><span data-stu-id="4a9cf-118">Select **X12 - Decode X12 message**.</span></span>
   
    ![Búsqueda de "x12"](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. <span data-ttu-id="4a9cf-120">Si previamente no creó ninguna conexión de cuenta de integración de tooyour, se te pedirá toocreate ahora esa conexión.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="4a9cf-121">Nombre de la conexión y seleccione cuenta de integración de Hola que desea tooconnect.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 

    ![Proporcionar los detalles de conexión de la cuenta de integración](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    <span data-ttu-id="4a9cf-123">Aquellas propiedades con un asterisco son obligatorias.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="4a9cf-124">Propiedad</span><span class="sxs-lookup"><span data-stu-id="4a9cf-124">Property</span></span> | <span data-ttu-id="4a9cf-125">Detalles</span><span class="sxs-lookup"><span data-stu-id="4a9cf-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="4a9cf-126">Nombre de la conexión *</span><span class="sxs-lookup"><span data-stu-id="4a9cf-126">Connection Name *</span></span> |<span data-ttu-id="4a9cf-127">Escriba cualquier nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="4a9cf-128">Cuenta de integración*</span><span class="sxs-lookup"><span data-stu-id="4a9cf-128">Integration Account *</span></span> |<span data-ttu-id="4a9cf-129">Escriba un nombre para la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-129">Enter a name for your integration account.</span></span> <span data-ttu-id="4a9cf-130">Asegúrese de que la aplicación de cuenta y la lógica de integración están en hello misma ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="4a9cf-131">Cuando haya terminado, los detalles de la conexión deben tener un aspecto similar ejemplo toothis.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="4a9cf-132">toofinish crear la conexión, elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![detalles de conexión de la cuenta de integración](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. <span data-ttu-id="4a9cf-134">Una vez creada la conexión, como se muestra en este ejemplo, seleccione toodecode de mensaje de archivo sin formato de hello X12.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-134">After your connection is created, as shown in this example, select hello X12 flat file message toodecode.</span></span>

    ![creación de la conexión de la cuenta de integración](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    <span data-ttu-id="4a9cf-136">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4a9cf-136">For example:</span></span>

    ![Seleccione el mensaje de archivo plano X12 para descodificar](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a><span data-ttu-id="4a9cf-138">Detalles de X12 Decode</span><span class="sxs-lookup"><span data-stu-id="4a9cf-138">X12 Decode details</span></span>

<span data-ttu-id="4a9cf-139">Conector de descodificación de Hello X12 lleva a cabo estas tareas:</span><span class="sxs-lookup"><span data-stu-id="4a9cf-139">hello X12 Decode connector performs these tasks:</span></span>

* <span data-ttu-id="4a9cf-140">Valida sobre hello en el acuerdo de socio comercial</span><span class="sxs-lookup"><span data-stu-id="4a9cf-140">Validates hello envelope against trading partner agreement</span></span>
* <span data-ttu-id="4a9cf-141">Valida propiedades EDI y específicas del asociado.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-141">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="4a9cf-142">Validación estructural de EDI y validación de esquema extendido</span><span class="sxs-lookup"><span data-stu-id="4a9cf-142">EDI structural validation, and extended schema validation</span></span>
  * <span data-ttu-id="4a9cf-143">Validación de la estructura de Hola de sobres de intercambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-143">Validation of hello structure of hello interchange envelope.</span></span>
  * <span data-ttu-id="4a9cf-144">Validación de esquemas de sobres de hello en el esquema de control de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-144">Schema validation of hello envelope against hello control schema.</span></span>
  * <span data-ttu-id="4a9cf-145">Validación de esquema de los elementos de datos de conjuntos de transacciones de hello en el esquema de mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-145">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="4a9cf-146">Validación de EDI realizada en los elementos de datos del conjunto de transacciones</span><span class="sxs-lookup"><span data-stu-id="4a9cf-146">EDI validation performed on transaction-set data elements</span></span> 
* <span data-ttu-id="4a9cf-147">Comprueba que los números de control de conjunto de intercambio, grupo y transacción hello no sean duplicados</span><span class="sxs-lookup"><span data-stu-id="4a9cf-147">Verifies that hello interchange, group, and transaction set control numbers are not duplicates</span></span>
  * <span data-ttu-id="4a9cf-148">Comprueba el número de control de intercambio de hello en los intercambios recibidos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-148">Checks hello interchange control number against previously received interchanges.</span></span>
  * <span data-ttu-id="4a9cf-149">Comprueba el número de control de grupo de hello con los otros números de control de grupo en el intercambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-149">Checks hello group control number against other group control numbers in hello interchange.</span></span>
  * <span data-ttu-id="4a9cf-150">Comprueba el número de control del conjunto de transacciones de hello en otros números de control de conjunto de transacciones de ese grupo.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-150">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="4a9cf-151">Hola Intercambio en conjuntos de transacciones se divide o conserva todo el intercambio hello:</span><span class="sxs-lookup"><span data-stu-id="4a9cf-151">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="4a9cf-152">Divide el intercambio como conjuntos de transacciones (suspende conjuntos de transacciones en caso de error): divide el intercambio en conjuntos de transacciones y analiza cada conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-152">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="4a9cf-153">acción de descodificación de Hello X12 envía solo esos conjuntos de transacciones que no superan la validación demasiado`badMessages`y genera Hola transacciones restantes se establece demasiado`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-153">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="4a9cf-154">Divide el intercambio como conjuntos de transacciones (suspende el intercambio en caso de error): divide el intercambio en conjuntos de transacciones y analiza cada conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-154">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="4a9cf-155">Si una o más conjuntos de transacciones en la validación de un error de intercambio de hello, acción de descodificación de hello X12 genera conjuntos de todas las transacciones de hello en dicho intercambio demasiado`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-155">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="4a9cf-156">Conservar intercambio: suspender conjuntos de transacciones en caso de error: conservar intercambio de Hola y proceso Hola todo el intercambio por lotes.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-156">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="4a9cf-157">acción de descodificación de Hello X12 envía solo esos conjuntos de transacciones que no superan la validación demasiado`badMessages`y genera Hola transacciones restantes se establece demasiado`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-157">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="4a9cf-158">Conservar intercambio: suspender intercambio en caso de error: conservar intercambio de Hola y proceso Hola todo el intercambio por lotes.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-158">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="4a9cf-159">Si una o más conjuntos de transacciones en la validación de un error de intercambio de hello, acción de descodificación de hello X12 genera conjuntos de todas las transacciones de hello en dicho intercambio demasiado`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-159">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span> 
* <span data-ttu-id="4a9cf-160">Genera una confirmación técnica o funcional (si esta opción está configurada).</span><span class="sxs-lookup"><span data-stu-id="4a9cf-160">Generates a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="4a9cf-161">Se genera una confirmación técnica como resultado de la validación del encabezado.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-161">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="4a9cf-162">Hola confirmación técnica informa del estado Hola Hola del procesamiento de un encabezado de intercambio y finalizador mediante receptor de direcciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-162">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver.</span></span>
  * <span data-ttu-id="4a9cf-163">Se genera una confirmación funcional como resultado de la validación del cuerpo.</span><span class="sxs-lookup"><span data-stu-id="4a9cf-163">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="4a9cf-164">confirmación funcional Hello notifica cada error al procesar Hola recibió el documento</span><span class="sxs-lookup"><span data-stu-id="4a9cf-164">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="4a9cf-165">Swagger de hello de vista</span><span class="sxs-lookup"><span data-stu-id="4a9cf-165">View hello swagger</span></span>
<span data-ttu-id="4a9cf-166">Vea hello [swagger detalles](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="4a9cf-166">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4a9cf-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4a9cf-167">Next steps</span></span>
[<span data-ttu-id="4a9cf-168">Obtener más información sobre Hola paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="4a9cf-168">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial") 

