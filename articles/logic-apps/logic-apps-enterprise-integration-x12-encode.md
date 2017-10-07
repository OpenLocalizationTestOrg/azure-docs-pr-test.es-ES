---
title: mensajes de aaaEncode X12 - Azure Logic Apps | Documentos de Microsoft
description: "Validar EDI y convertir la codificación XML mensajes con X12 mensaje codificador Hola paquete de integración empresarial para las aplicaciones lógicas de Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="d5062-103">Codificar X12 mensajes para las aplicaciones lógicas de Azure con hello paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="d5062-103">Encode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="d5062-104">Con el conector de mensaje de Hola Encode X12, puede validar EDI y propiedades específicas del partner, convertir los mensajes codificados en XML en conjuntos de transacciones EDI en el intercambio de Hola y solicitar una confirmación técnica, la confirmación funcional o ambos.</span><span class="sxs-lookup"><span data-stu-id="d5062-104">With hello Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in hello interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="d5062-105">toouse este conector, debe agregar Hola conector tooan existente desencadenador en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="d5062-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="d5062-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="d5062-106">Before you start</span></span>

<span data-ttu-id="d5062-107">Aquí es elementos de Hola que necesita:</span><span class="sxs-lookup"><span data-stu-id="d5062-107">Here's hello items you need:</span></span>

* <span data-ttu-id="d5062-108">Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="d5062-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="d5062-109">Una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md) que ya esté definida y asociada a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5062-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="d5062-110">Debe tener un conector integración cuenta toouse Hola Encode X12 mensaje.</span><span class="sxs-lookup"><span data-stu-id="d5062-110">You must have an integration account toouse hello Encode X12 message connector.</span></span>
* <span data-ttu-id="d5062-111">Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="d5062-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="d5062-112">Un [contrato X12](logic-apps-enterprise-integration-x12.md) ya definido en su cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="d5062-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="d5062-113">Codificación de mensajes X12</span><span class="sxs-lookup"><span data-stu-id="d5062-113">Encode X12 messages</span></span>

1. <span data-ttu-id="d5062-114">[Creación de una aplicación lógica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d5062-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="d5062-115">Conector de mensaje de Hola Encode X12 no tiene desencadenadores, por lo que debe agregar un desencadenador para iniciar la aplicación lógica, como un desencadenador de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="d5062-115">hello Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="d5062-116">Hola diseñador la lógica de aplicación, agregar un desencadenador y, a continuación, agregar una aplicación de lógica de tooyour de acción.</span><span class="sxs-lookup"><span data-stu-id="d5062-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="d5062-117">En el cuadro de búsqueda de hello, escriba "x12" para el filtro.</span><span class="sxs-lookup"><span data-stu-id="d5062-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="d5062-118">Seleccione **X12-codificar los mensajes tooX12 por el nombre del contrato** o **X12-codificar tooX12 mensaje identidades**.</span><span class="sxs-lookup"><span data-stu-id="d5062-118">Select either **X12 - Encode tooX12 message by agreement name** or **X12 - Encode tooX12 message by identities**.</span></span>
   
    ![Búsqueda de "x12"](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="d5062-120">Si previamente no creó ninguna conexión de cuenta de integración de tooyour, se te pedirá toocreate ahora esa conexión.</span><span class="sxs-lookup"><span data-stu-id="d5062-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="d5062-121">Nombre de la conexión y seleccione cuenta de integración de Hola que desea tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d5062-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![conexión de la cuenta de integración](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="d5062-123">Aquellas propiedades con un asterisco son obligatorias.</span><span class="sxs-lookup"><span data-stu-id="d5062-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="d5062-124">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d5062-124">Property</span></span> | <span data-ttu-id="d5062-125">Detalles</span><span class="sxs-lookup"><span data-stu-id="d5062-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="d5062-126">Nombre de la conexión *</span><span class="sxs-lookup"><span data-stu-id="d5062-126">Connection Name *</span></span> |<span data-ttu-id="d5062-127">Escriba cualquier nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="d5062-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="d5062-128">Cuenta de integración*</span><span class="sxs-lookup"><span data-stu-id="d5062-128">Integration Account *</span></span> |<span data-ttu-id="d5062-129">Escriba un nombre para la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="d5062-129">Enter a name for your integration account.</span></span> <span data-ttu-id="d5062-130">Asegúrese de que la aplicación de cuenta y la lógica de integración están en hello misma ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5062-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="d5062-131">Cuando haya terminado, los detalles de la conexión deben tener un aspecto similar ejemplo toothis.</span><span class="sxs-lookup"><span data-stu-id="d5062-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="d5062-132">toofinish crear la conexión, elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="d5062-132">toofinish creating your connection, choose **Create**.</span></span>

    ![creación de la conexión de la cuenta de integración](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="d5062-134">La conexión se ha creado.</span><span class="sxs-lookup"><span data-stu-id="d5062-134">Your connection is now created.</span></span>

    ![detalles de conexión de la cuenta de integración](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="d5062-136">Encode X12 Message por nombre de acuerdo</span><span class="sxs-lookup"><span data-stu-id="d5062-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="d5062-137">Si ha elegido tooencode X12 mensajes por nombre de contrato, abra hello **nombre de X12 acuerdo** lista, escriba o seleccione el X12 existente acuerdo.</span><span class="sxs-lookup"><span data-stu-id="d5062-137">If you chose tooencode X12 messages by agreement name, open hello **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="d5062-138">Escriba tooencode de mensaje de Hola XML.</span><span class="sxs-lookup"><span data-stu-id="d5062-138">Enter hello XML message tooencode.</span></span>

![Escriba X12 tooencode de mensajes XML y el nombre de contrato](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="d5062-140">Encode X12 Message por identidades</span><span class="sxs-lookup"><span data-stu-id="d5062-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="d5062-141">Si elige tooencode X12 mensajes para las identidades, escriba el identificador del remitente de hello, calificador de remitente, identificador de receptor y calificador de receptor como está configurado en su X12 acuerdo.</span><span class="sxs-lookup"><span data-stu-id="d5062-141">If you choose tooencode X12 messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="d5062-142">Seleccione tooencode de mensaje de Hola XML.</span><span class="sxs-lookup"><span data-stu-id="d5062-142">Select hello XML message tooencode.</span></span>
   
![Proporcione las identidades de remitente y receptor, seleccione tooencode de mensaje XML](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="d5062-144">Detalles de la codificación de X12</span><span class="sxs-lookup"><span data-stu-id="d5062-144">X12 Encode details</span></span>

<span data-ttu-id="d5062-145">Hola X12 Encode conector lleva a cabo estas tareas:</span><span class="sxs-lookup"><span data-stu-id="d5062-145">hello X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="d5062-146">Resolución del acuerdo haciendo coincidir las propiedades de contexto de remitente y receptor.</span><span class="sxs-lookup"><span data-stu-id="d5062-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="d5062-147">Serializa el intercambio EDI de hello, convertir los mensajes codificados en XML en conjuntos de transacciones EDI en el intercambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5062-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="d5062-148">Aplica segmentos de encabezado y finalizador del conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="d5062-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="d5062-149">Genera un número de control de intercambio, un número de control de grupo y un número de control del conjunto de transacciones para cada intercambio de salida.</span><span class="sxs-lookup"><span data-stu-id="d5062-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="d5062-150">Reemplaza los separadores en datos de carga de Hola</span><span class="sxs-lookup"><span data-stu-id="d5062-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="d5062-151">Valida propiedades EDI y específicas del asociado.</span><span class="sxs-lookup"><span data-stu-id="d5062-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="d5062-152">Validación de esquema de los elementos de datos de conjuntos de transacciones de hello en mensajes de bienvenida del esquema</span><span class="sxs-lookup"><span data-stu-id="d5062-152">Schema validation of hello transaction-set data elements against hello message Schema</span></span>
  * <span data-ttu-id="d5062-153">Validación de EDI realizada en los elementos de datos del conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="d5062-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="d5062-154">Validación extendida realizada en los elementos de datos del conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="d5062-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="d5062-155">Solicita una confirmación técnica o funcional (si esta opción está configurada).</span><span class="sxs-lookup"><span data-stu-id="d5062-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="d5062-156">Se genera una confirmación técnica como resultado de la validación del encabezado.</span><span class="sxs-lookup"><span data-stu-id="d5062-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="d5062-157">Hola confirmación técnica informa Hola del estado de procesamiento de Hola de un encabezado de intercambio y finalizador mediante el receptor de direcciones de Hola</span><span class="sxs-lookup"><span data-stu-id="d5062-157">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver</span></span>
  * <span data-ttu-id="d5062-158">Se genera una confirmación funcional como resultado de la validación del cuerpo.</span><span class="sxs-lookup"><span data-stu-id="d5062-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="d5062-159">confirmación funcional Hello notifica cada error al procesar Hola recibió el documento</span><span class="sxs-lookup"><span data-stu-id="d5062-159">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="d5062-160">Swagger de hello de vista</span><span class="sxs-lookup"><span data-stu-id="d5062-160">View hello swagger</span></span>
<span data-ttu-id="d5062-161">Vea hello [swagger detalles](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="d5062-161">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d5062-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d5062-162">Next steps</span></span>
[<span data-ttu-id="d5062-163">Obtener más información sobre Hola paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="d5062-163">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial") 

