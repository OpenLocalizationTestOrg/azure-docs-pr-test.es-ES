---
title: "Codificación de mensajes EDIFACT: Azure Logic Apps | Microsoft Docs"
description: Valide EDI y genere XML con el codificador de mensajes EDIFACT en Enterprise Integration Pack para Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b8d577326d23ec45cb4a9ec0e450ebf7afd945f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="96f22-103">Codificación de mensajes EDIFACT para Azure Logic Apps con Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="96f22-103">Encode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="96f22-104">Con el conector de codificación de mensajes EDIFACT puede validar EDI y propiedades específicas del asociado, generar un documento XML para cada conjunto de transacciones y solicitar la confirmación técnica, la funcional o ambas.</span><span class="sxs-lookup"><span data-stu-id="96f22-104">With the Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="96f22-105">Para usar este conector, debe agregarlo a un desencadenador existente en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="96f22-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="96f22-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="96f22-106">Before you start</span></span>

<span data-ttu-id="96f22-107">Esto es lo que necesita:</span><span class="sxs-lookup"><span data-stu-id="96f22-107">Here's the items you need:</span></span>

* <span data-ttu-id="96f22-108">Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="96f22-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="96f22-109">Una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md) que ya esté definida y asociada a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="96f22-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="96f22-110">Debe tener una cuenta de integración para usar el conector de codificación de mensajes EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="96f22-110">You must have an integration account to use the Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="96f22-111">Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="96f22-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="96f22-112">Un [contrato EDIFACT](logic-apps-enterprise-integration-edifact.md) ya definido en la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="96f22-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="96f22-113">Codificación de mensajes EDIFACT</span><span class="sxs-lookup"><span data-stu-id="96f22-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="96f22-114">[Creación de una aplicación lógica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="96f22-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="96f22-115">El conector de codificación de mensajes EDIFACT no tiene desencadenadores, por lo que debe agregar uno para iniciar la aplicación lógica, por ejemplo, un desencadenador de solicitud.</span><span class="sxs-lookup"><span data-stu-id="96f22-115">The Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="96f22-116">En el Diseñador de aplicaciones lógicas, agregue un desencadenador y una acción a la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="96f22-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="96f22-117">En el cuadro de búsqueda, escriba "EDIFACT" para el filtro.</span><span class="sxs-lookup"><span data-stu-id="96f22-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="96f22-118">Seleccione **Encode EDIFACT Message by agreement name** (Codificación de mensajes EDIFACT por nombre de contrato) o **Encode to EDIFACT Message by identities** (Codificación de mensajes EDIFACT por identidad).</span><span class="sxs-lookup"><span data-stu-id="96f22-118">Select either **Encode EDIFACT Message by agreement name** or **Encode to EDIFACT message by identities**.</span></span>
   
    ![buscar EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="96f22-120">Si no había creado ninguna conexión a la cuenta de integración, se le pedirá que lo haga ahora.</span><span class="sxs-lookup"><span data-stu-id="96f22-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="96f22-121">Asigne un nombre a la conexión y seleccione la cuenta de integración que desee conectar.</span><span class="sxs-lookup"><span data-stu-id="96f22-121">Name your connection, and select the integration account that you want to connect.</span></span>

    ![crear la conexión de la cuenta de integración](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="96f22-123">Aquellas propiedades con un asterisco son obligatorias.</span><span class="sxs-lookup"><span data-stu-id="96f22-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="96f22-124">Propiedad</span><span class="sxs-lookup"><span data-stu-id="96f22-124">Property</span></span> | <span data-ttu-id="96f22-125">Detalles</span><span class="sxs-lookup"><span data-stu-id="96f22-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="96f22-126">Nombre de la conexión *</span><span class="sxs-lookup"><span data-stu-id="96f22-126">Connection Name *</span></span> |<span data-ttu-id="96f22-127">Escriba cualquier nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="96f22-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="96f22-128">Cuenta de integración*</span><span class="sxs-lookup"><span data-stu-id="96f22-128">Integration Account *</span></span> |<span data-ttu-id="96f22-129">Escriba un nombre para la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="96f22-129">Enter a name for your integration account.</span></span> <span data-ttu-id="96f22-130">Asegúrese de que la cuenta de integración y la aplicación lógica se encuentren en la misma ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="96f22-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="96f22-131">Cuando haya terminado, los detalles de la conexión deberían parecerse a este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="96f22-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="96f22-132">Para terminar de crear la conexión, elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="96f22-132">To finish creating your connection, choose **Create**.</span></span>

    ![detalles de conexión de la cuenta de integración](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="96f22-134">La conexión se ha creado.</span><span class="sxs-lookup"><span data-stu-id="96f22-134">Your connection is now created.</span></span>

    ![creación de la conexión de la cuenta de integración](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="96f22-136">Encode EDIFACT Message por nombre del acuerdo</span><span class="sxs-lookup"><span data-stu-id="96f22-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="96f22-137">Si decide codificar mensajes EDIFACT por nombre de contrato, abra la lista **Nombre del contrato EDIFACT** y escriba o seleccione el nombre del contrato EDIFACT existente.</span><span class="sxs-lookup"><span data-stu-id="96f22-137">If you chose to encode EDIFACT messages by agreement name, open the **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="96f22-138">Escriba el mensaje XML para codificar.</span><span class="sxs-lookup"><span data-stu-id="96f22-138">Enter the XML message to encode.</span></span>

![Escriba el nombre del contrato EDIFACT y el mensaje XML para codificar.](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="96f22-140">Encode EDIFACT Message por identidades</span><span class="sxs-lookup"><span data-stu-id="96f22-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="96f22-141">Si elige codificar mensajes EDIFACT por identidad, especifique el identificador y el calificador del remitente, así como el identificador y el calificador del receptor, tal y como están configurados en el contrato EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="96f22-141">If you choose to encode EDIFACT messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="96f22-142">Seleccione el mensaje XML para codificar.</span><span class="sxs-lookup"><span data-stu-id="96f22-142">Select the XML message to encode.</span></span>

![Proporcione la identidad del remitente y del receptor, y seleccione el mensaje XML para codificar.](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="96f22-144">Detalles de la codificación de EDIFACT</span><span class="sxs-lookup"><span data-stu-id="96f22-144">EDIFACT Encode details</span></span>

<span data-ttu-id="96f22-145">El conector de codificación EDIFACT lleva a cabo estas tareas:</span><span class="sxs-lookup"><span data-stu-id="96f22-145">The Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="96f22-146">Resolver el acuerdo haciendo coincidir el calificador y el identificador del remitente con el calificador y el identificador del receptor del receptor.</span><span class="sxs-lookup"><span data-stu-id="96f22-146">Resolve the agreement by matching the sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="96f22-147">Serializa el intercambio EDI, convirtiendo los mensajes codificados en XML en conjuntos de transacciones EDI en el intercambio.</span><span class="sxs-lookup"><span data-stu-id="96f22-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="96f22-148">Aplica segmentos de encabezado y finalizador del conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="96f22-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="96f22-149">Genera un número de control de intercambio, un número de control de grupo y un número de control del conjunto de transacciones para cada intercambio de salida.</span><span class="sxs-lookup"><span data-stu-id="96f22-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="96f22-150">Reemplaza los separadores en los datos de carga útil.</span><span class="sxs-lookup"><span data-stu-id="96f22-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="96f22-151">Valida propiedades EDI y específicas del asociado.</span><span class="sxs-lookup"><span data-stu-id="96f22-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="96f22-152">Validación del esquema de los elementos de datos del conjunto de transacciones con respecto al esquema de mensaje.</span><span class="sxs-lookup"><span data-stu-id="96f22-152">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="96f22-153">Validación de EDI realizada en los elementos de datos del conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="96f22-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="96f22-154">Validación extendida realizada en los elementos de datos del conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="96f22-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="96f22-155">Genera un documento XML para cada conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="96f22-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="96f22-156">Solicita una confirmación técnica o funcional (si esta opción está configurada).</span><span class="sxs-lookup"><span data-stu-id="96f22-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="96f22-157">Como confirmación técnica, el mensaje CONTRL indica la recepción de un intercambio.</span><span class="sxs-lookup"><span data-stu-id="96f22-157">As a technical acknowledgment, the CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="96f22-158">Como confirmación funcional, el mensaje CONTRL indica la aceptación o el rechazo del intercambio, el grupo o el mensaje recibido, con una lista de errores o una funcionalidad no admitida.</span><span class="sxs-lookup"><span data-stu-id="96f22-158">As a functional acknowledgment, the CONTRL message indicates acceptance or rejection of the received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="96f22-159">Ver el archivo de Swagger</span><span class="sxs-lookup"><span data-stu-id="96f22-159">View Swagger file</span></span>
<span data-ttu-id="96f22-160">Para ver los detalles de Swagger para el conector EDIFACT, consulte [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="96f22-160">To view the Swagger details for the EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="96f22-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="96f22-161">Next steps</span></span>
[<span data-ttu-id="96f22-162">Más información sobre Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="96f22-162">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Información sobre Enterprise Integration Pack") 

