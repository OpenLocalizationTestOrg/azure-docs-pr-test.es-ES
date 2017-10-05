---
title: "Codificación de mensajes X12: Azure Logic Apps | Microsoft Docs"
description: "Valide EDI y convierta mensajes con codificación XML con el codificador de mensajes X12 en Enterprise Integration Pack para Azure Logic Apps"
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
ms.openlocfilehash: 29d19364b9a98e351c95f13e68a2e63b9f6439f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="1265a-103">Codificación de mensajes X12 para Azure Logic Apps con Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="1265a-103">Encode X12 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="1265a-104">Con el conector de codificación de mensajes X12, puede validar propiedades EDI y específicas del asociado, convertir mensajes con codificación XML en conjuntos de transacciones EDI en el intercambio y solicitar una confirmación técnica, una funcional o ambas.</span><span class="sxs-lookup"><span data-stu-id="1265a-104">With the Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in the interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="1265a-105">Para usar este conector, debe agregarlo a un desencadenador existente en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="1265a-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="1265a-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="1265a-106">Before you start</span></span>

<span data-ttu-id="1265a-107">Esto es lo que necesita:</span><span class="sxs-lookup"><span data-stu-id="1265a-107">Here's the items you need:</span></span>

* <span data-ttu-id="1265a-108">Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="1265a-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="1265a-109">Una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md) que ya esté definida y asociada a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1265a-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="1265a-110">Debe tener una cuenta de integración para usar el conector de codificación de mensajes X12.</span><span class="sxs-lookup"><span data-stu-id="1265a-110">You must have an integration account to use the Encode X12 message connector.</span></span>
* <span data-ttu-id="1265a-111">Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="1265a-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="1265a-112">Un [contrato X12](logic-apps-enterprise-integration-x12.md) ya definido en su cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="1265a-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="1265a-113">Codificación de mensajes X12</span><span class="sxs-lookup"><span data-stu-id="1265a-113">Encode X12 messages</span></span>

1. <span data-ttu-id="1265a-114">[Creación de una aplicación lógica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1265a-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="1265a-115">El conector de codificación de mensajes X12 no tiene desencadenadores, por lo que debe agregar uno para iniciar la aplicación lógica, como un desencadenador de solicitud.</span><span class="sxs-lookup"><span data-stu-id="1265a-115">The Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="1265a-116">En el Diseñador de aplicaciones lógicas, agregue un desencadenador y una acción a la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="1265a-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="1265a-117">En el cuadro de búsqueda, escriba "x12" para el filtro.</span><span class="sxs-lookup"><span data-stu-id="1265a-117">In the search box, enter "x12" for your filter.</span></span> <span data-ttu-id="1265a-118">Seleccione **X12 - Codificar en mensaje X12 por nombre de contrato** o **X12 - Codificar en mensaje X12 por identidades**.</span><span class="sxs-lookup"><span data-stu-id="1265a-118">Select either **X12 - Encode to X12 message by agreement name** or **X12 - Encode to X12 message by identities**.</span></span>
   
    ![Búsqueda de "x12"](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="1265a-120">Si no había creado ninguna conexión a la cuenta de integración, se le pedirá que lo haga ahora.</span><span class="sxs-lookup"><span data-stu-id="1265a-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="1265a-121">Asigne un nombre a la conexión y seleccione la cuenta de integración que desee conectar.</span><span class="sxs-lookup"><span data-stu-id="1265a-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![conexión de la cuenta de integración](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="1265a-123">Aquellas propiedades con un asterisco son obligatorias.</span><span class="sxs-lookup"><span data-stu-id="1265a-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="1265a-124">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1265a-124">Property</span></span> | <span data-ttu-id="1265a-125">Detalles</span><span class="sxs-lookup"><span data-stu-id="1265a-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="1265a-126">Nombre de la conexión *</span><span class="sxs-lookup"><span data-stu-id="1265a-126">Connection Name *</span></span> |<span data-ttu-id="1265a-127">Escriba cualquier nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="1265a-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="1265a-128">Cuenta de integración*</span><span class="sxs-lookup"><span data-stu-id="1265a-128">Integration Account *</span></span> |<span data-ttu-id="1265a-129">Escriba un nombre para la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="1265a-129">Enter a name for your integration account.</span></span> <span data-ttu-id="1265a-130">Asegúrese de que la cuenta de integración y la aplicación lógica se encuentren en la misma ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="1265a-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="1265a-131">Cuando haya terminado, los detalles de la conexión deberían parecerse a este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1265a-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="1265a-132">Para terminar de crear la conexión, elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1265a-132">To finish creating your connection, choose **Create**.</span></span>

    ![creación de la conexión de la cuenta de integración](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="1265a-134">La conexión se ha creado.</span><span class="sxs-lookup"><span data-stu-id="1265a-134">Your connection is now created.</span></span>

    ![detalles de conexión de la cuenta de integración](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="1265a-136">Encode X12 Message por nombre de acuerdo</span><span class="sxs-lookup"><span data-stu-id="1265a-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="1265a-137">Si decide codificar mensajes X12 por nombre de contrato, abra la lista **Nombre del contrato X12** y escriba o seleccione el contrato X12 existente.</span><span class="sxs-lookup"><span data-stu-id="1265a-137">If you chose to encode X12 messages by agreement name, open the **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="1265a-138">Escriba el mensaje XML para codificar.</span><span class="sxs-lookup"><span data-stu-id="1265a-138">Enter the XML message to encode.</span></span>

![Escriba el nombre del contrato X12 y el mensaje XML para codificar](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="1265a-140">Encode X12 Message por identidades</span><span class="sxs-lookup"><span data-stu-id="1265a-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="1265a-141">Si elige codificar mensajes X12 por identidades, especifique el identificador y el calificador del remitente, así como el identificador y el calificador del receptor, tal y como están configurados en el contrato X12.</span><span class="sxs-lookup"><span data-stu-id="1265a-141">If you choose to encode X12 messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="1265a-142">Seleccione el mensaje XML para codificar.</span><span class="sxs-lookup"><span data-stu-id="1265a-142">Select the XML message to encode.</span></span>
   
![Proporcione la identidad del remitente y del receptor, y seleccione el mensaje XML para codificar.](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="1265a-144">Detalles de la codificación de X12</span><span class="sxs-lookup"><span data-stu-id="1265a-144">X12 Encode details</span></span>

<span data-ttu-id="1265a-145">El conector de codificación X12 lleva a cabo estas tareas:</span><span class="sxs-lookup"><span data-stu-id="1265a-145">The X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="1265a-146">Resolución del acuerdo haciendo coincidir las propiedades de contexto de remitente y receptor.</span><span class="sxs-lookup"><span data-stu-id="1265a-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="1265a-147">Serializa el intercambio EDI, convirtiendo los mensajes codificados en XML en conjuntos de transacciones EDI en el intercambio.</span><span class="sxs-lookup"><span data-stu-id="1265a-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="1265a-148">Aplica segmentos de encabezado y finalizador del conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="1265a-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="1265a-149">Genera un número de control de intercambio, un número de control de grupo y un número de control del conjunto de transacciones para cada intercambio de salida.</span><span class="sxs-lookup"><span data-stu-id="1265a-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="1265a-150">Reemplaza los separadores en los datos de carga útil.</span><span class="sxs-lookup"><span data-stu-id="1265a-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="1265a-151">Valida propiedades EDI y específicas del asociado.</span><span class="sxs-lookup"><span data-stu-id="1265a-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="1265a-152">Validación del esquema de los elementos de datos del conjunto de transacciones con respecto al esquema de mensaje.</span><span class="sxs-lookup"><span data-stu-id="1265a-152">Schema validation of the transaction-set data elements against the message Schema</span></span>
  * <span data-ttu-id="1265a-153">Validación de EDI realizada en los elementos de datos del conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="1265a-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="1265a-154">Validación extendida realizada en los elementos de datos del conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="1265a-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="1265a-155">Solicita una confirmación técnica o funcional (si esta opción está configurada).</span><span class="sxs-lookup"><span data-stu-id="1265a-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="1265a-156">Se genera una confirmación técnica como resultado de la validación del encabezado.</span><span class="sxs-lookup"><span data-stu-id="1265a-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="1265a-157">La confirmación técnica informa del estado del procesamiento de un encabezado y finalizador de intercambio por parte del receptor de la dirección.</span><span class="sxs-lookup"><span data-stu-id="1265a-157">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver</span></span>
  * <span data-ttu-id="1265a-158">Se genera una confirmación funcional como resultado de la validación del cuerpo.</span><span class="sxs-lookup"><span data-stu-id="1265a-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="1265a-159">La confirmación funcional informa de cada error encontrado al procesar el documento recibido.</span><span class="sxs-lookup"><span data-stu-id="1265a-159">The functional acknowledgment reports each error encountered while processing the received document</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="1265a-160">Visualización de Swagger</span><span class="sxs-lookup"><span data-stu-id="1265a-160">View the swagger</span></span>
<span data-ttu-id="1265a-161">Vea los [detalles de Swagger](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="1265a-161">See the [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1265a-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1265a-162">Next steps</span></span>
[<span data-ttu-id="1265a-163">Más información sobre Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="1265a-163">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Información sobre Enterprise Integration Pack") 

