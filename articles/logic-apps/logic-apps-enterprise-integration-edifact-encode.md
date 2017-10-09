---
title: mensajes EDIFACT aaaEncode - Azure Logic Apps | Documentos de Microsoft
description: "Validar EDI y generar XML con el codificador de mensajes EDIFACT en hello paquete de integración empresarial para las aplicaciones lógicas de Azure"
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
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="bc1f4-103">Codificar los mensajes EDIFACT para las aplicaciones lógicas de Azure con hello paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="bc1f4-103">Encode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="bc1f4-104">Con el conector de mensaje de Hola codificar EDIFACT, puede validar EDI y propiedades específicas del partner, generar un documento XML para cada conjunto de transacciones y solicitar una confirmación técnica, la confirmación funcional o ambos.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-104">With hello Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="bc1f4-105">toouse este conector, debe agregar Hola conector tooan existente desencadenador en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="bc1f4-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="bc1f4-106">Before you start</span></span>

<span data-ttu-id="bc1f4-107">Aquí es elementos de Hola que necesita:</span><span class="sxs-lookup"><span data-stu-id="bc1f4-107">Here's hello items you need:</span></span>

* <span data-ttu-id="bc1f4-108">Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="bc1f4-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="bc1f4-109">Una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md) que ya esté definida y asociada a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="bc1f4-110">Debe tener un conector de mensaje integración cuenta toouse Hola codificar EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-110">You must have an integration account toouse hello Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="bc1f4-111">Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="bc1f4-112">Un [contrato EDIFACT](logic-apps-enterprise-integration-edifact.md) ya definido en la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="bc1f4-113">Codificación de mensajes EDIFACT</span><span class="sxs-lookup"><span data-stu-id="bc1f4-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="bc1f4-114">[Creación de una aplicación lógica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="bc1f4-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="bc1f4-115">Conector de mensaje de Hola codificar EDIFACT no tiene desencadenadores, por lo que debe agregar un desencadenador para iniciar la aplicación lógica, como un desencadenador de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-115">hello Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="bc1f4-116">Hola diseñador la lógica de aplicación, agregar un desencadenador y, a continuación, agregar una aplicación de lógica de tooyour de acción.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="bc1f4-117">En el cuadro de búsqueda de hello, escriba "EDIFACT" como filtro.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="bc1f4-118">Seleccione **codificar mensaje EDIFACT por el nombre del contrato** o **Encode tooEDIFACT mensaje identidades**.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-118">Select either **Encode EDIFACT Message by agreement name** or **Encode tooEDIFACT message by identities**.</span></span>
   
    ![buscar EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="bc1f4-120">Si previamente no creó ninguna conexión de cuenta de integración de tooyour, se te pedirá toocreate ahora esa conexión.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="bc1f4-121">Nombre de la conexión y seleccione cuenta de integración de Hola que desea tooconnect.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>

    ![crear la conexión de la cuenta de integración](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="bc1f4-123">Aquellas propiedades con un asterisco son obligatorias.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="bc1f4-124">Propiedad</span><span class="sxs-lookup"><span data-stu-id="bc1f4-124">Property</span></span> | <span data-ttu-id="bc1f4-125">Detalles</span><span class="sxs-lookup"><span data-stu-id="bc1f4-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="bc1f4-126">Nombre de la conexión *</span><span class="sxs-lookup"><span data-stu-id="bc1f4-126">Connection Name *</span></span> |<span data-ttu-id="bc1f4-127">Escriba cualquier nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="bc1f4-128">Cuenta de integración*</span><span class="sxs-lookup"><span data-stu-id="bc1f4-128">Integration Account *</span></span> |<span data-ttu-id="bc1f4-129">Escriba un nombre para la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-129">Enter a name for your integration account.</span></span> <span data-ttu-id="bc1f4-130">Asegúrese de que la aplicación de cuenta y la lógica de integración están en hello misma ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="bc1f4-131">Cuando haya terminado, los detalles de la conexión deben tener un aspecto similar ejemplo toothis.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="bc1f4-132">toofinish crear la conexión, elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-132">toofinish creating your connection, choose **Create**.</span></span>

    ![detalles de conexión de la cuenta de integración](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="bc1f4-134">La conexión se ha creado.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-134">Your connection is now created.</span></span>

    ![creación de la conexión de la cuenta de integración](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="bc1f4-136">Encode EDIFACT Message por nombre del acuerdo</span><span class="sxs-lookup"><span data-stu-id="bc1f4-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="bc1f4-137">Si ha elegido tooencode mensajes EDIFACT por nombre de contrato, abra hello **acuerdo nombre de EDIFACT** lista, escriba o seleccione el nombre del acuerdo de EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-137">If you chose tooencode EDIFACT messages by agreement name, open hello **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="bc1f4-138">Escriba tooencode de mensaje de Hola XML.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-138">Enter hello XML message tooencode.</span></span>

![Escriba el nombre del acuerdo de EDIFACT y tooencode de mensaje XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="bc1f4-140">Encode EDIFACT Message por identidades</span><span class="sxs-lookup"><span data-stu-id="bc1f4-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="bc1f4-141">Si elige tooencode mensajes EDIFACT para las identidades, escriba el identificador de remitente de hello, calificador de remitente, identificador de receptor y el calificador de receptor como está configurado en el acuerdo de EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-141">If you choose tooencode EDIFACT messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="bc1f4-142">Seleccione tooencode de mensaje de Hola XML.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-142">Select hello XML message tooencode.</span></span>

![Proporcione las identidades de remitente y receptor, seleccione tooencode de mensaje XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="bc1f4-144">Detalles de la codificación de EDIFACT</span><span class="sxs-lookup"><span data-stu-id="bc1f4-144">EDIFACT Encode details</span></span>

<span data-ttu-id="bc1f4-145">Hola codificar EDIFACT conector lleva a cabo estas tareas:</span><span class="sxs-lookup"><span data-stu-id="bc1f4-145">hello Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="bc1f4-146">Resolver el acuerdo de hello haciendo coincidir el calificador de remitente de hello & identificador y calificador e identificador</span><span class="sxs-lookup"><span data-stu-id="bc1f4-146">Resolve hello agreement by matching hello sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="bc1f4-147">Serializa el intercambio EDI de hello, convertir los mensajes codificados en XML en conjuntos de transacciones EDI en el intercambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="bc1f4-148">Aplica segmentos de encabezado y finalizador del conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="bc1f4-149">Genera un número de control de intercambio, un número de control de grupo y un número de control del conjunto de transacciones para cada intercambio de salida.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="bc1f4-150">Reemplaza los separadores en datos de carga de Hola</span><span class="sxs-lookup"><span data-stu-id="bc1f4-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="bc1f4-151">Valida propiedades EDI y específicas del asociado.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="bc1f4-152">Validación de esquema de los elementos de datos de conjuntos de transacciones de hello en el esquema de mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-152">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="bc1f4-153">Validación de EDI realizada en los elementos de datos del conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="bc1f4-154">Validación extendida realizada en los elementos de datos del conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="bc1f4-155">Genera un documento XML para cada conjunto de transacciones.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="bc1f4-156">Solicita una confirmación técnica o funcional (si esta opción está configurada).</span><span class="sxs-lookup"><span data-stu-id="bc1f4-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="bc1f4-157">Como confirmación técnica, mensaje de bienvenida de CONTRL indica la recepción de un intercambio.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-157">As a technical acknowledgment, hello CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="bc1f4-158">Como una confirmación funcional, mensaje de bienvenida de CONTRL indica la aceptación o rechazo del intercambio de hello recibido, grupo o los mensajes, con una lista de errores o funcionalidad no admitida</span><span class="sxs-lookup"><span data-stu-id="bc1f4-158">As a functional acknowledgment, hello CONTRL message indicates acceptance or rejection of hello received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="bc1f4-159">Ver el archivo de Swagger</span><span class="sxs-lookup"><span data-stu-id="bc1f4-159">View Swagger file</span></span>
<span data-ttu-id="bc1f4-160">detalles de Swagger de tooview hello para el conector de saludo EDIFACT, vea [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="bc1f4-160">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc1f4-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bc1f4-161">Next steps</span></span>
[<span data-ttu-id="bc1f4-162">Obtener más información sobre Hola paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="bc1f4-162">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial") 

