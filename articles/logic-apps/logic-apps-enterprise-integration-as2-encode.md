---
title: "Codificación de mensajes AS2: Azure Logic Apps | Microsoft Docs"
description: Uso del codificador AS2 en Enterprise Integration Pack para Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 7889bf9e4e02143b6bb4c797531afa54f8647ce5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="6809f-103">Codificación de mensajes AS2 para Azure Logic Apps con Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="6809f-103">Encode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="6809f-104">Utilice el conector de codificación de mensajes AS2 para garantizar la seguridad y confiabilidad al transmitir mensajes.</span><span class="sxs-lookup"><span data-stu-id="6809f-104">To establish security and reliability while transmitting messages, use the Encode AS2 message connector.</span></span> <span data-ttu-id="6809f-105">Este conector ofrece firma digital, cifrado y confirmaciones mediante las notificaciones de disposición del mensaje (MDN), lo que también conlleva compatibilidad con la recepción sin rechazo.</span><span class="sxs-lookup"><span data-stu-id="6809f-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads to support for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="6809f-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="6809f-106">Before you start</span></span>

<span data-ttu-id="6809f-107">Esto es lo que necesita:</span><span class="sxs-lookup"><span data-stu-id="6809f-107">Here's the items you need:</span></span>

* <span data-ttu-id="6809f-108">Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="6809f-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="6809f-109">Una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md) que ya esté definida y asociada a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="6809f-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="6809f-110">Debe tener una cuenta de integración para usar el conector de codificación de mensajes AS2.</span><span class="sxs-lookup"><span data-stu-id="6809f-110">You must have an integration account to use the Encode AS2 message connector.</span></span>
* <span data-ttu-id="6809f-111">Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="6809f-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="6809f-112">Un [contrato AS2](logic-apps-enterprise-integration-as2.md) ya definido en la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="6809f-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="6809f-113">Codificación de mensajes AS2</span><span class="sxs-lookup"><span data-stu-id="6809f-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="6809f-114">[Creación de una aplicación lógica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6809f-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="6809f-115">El conector de codificación de mensajes AS2 no tiene desencadenadores, por lo que debe agregar uno para iniciar la aplicación lógica, por ejemplo, un desencadenador de solicitud.</span><span class="sxs-lookup"><span data-stu-id="6809f-115">The Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="6809f-116">En el Diseñador de aplicaciones lógicas, agregue un desencadenador y una acción a la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="6809f-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="6809f-117">En el cuadro de búsqueda, escriba "AS2" para el filtro.</span><span class="sxs-lookup"><span data-stu-id="6809f-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="6809f-118">Seleccione **AS2 – Encode AS2 Message** (AS2: codificación de mensajes AS2).</span><span class="sxs-lookup"><span data-stu-id="6809f-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    ![Búsqueda de "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="6809f-120">Si no había creado ninguna conexión a la cuenta de integración, se le pedirá que lo haga ahora.</span><span class="sxs-lookup"><span data-stu-id="6809f-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="6809f-121">Asigne un nombre a la conexión y seleccione la cuenta de integración que desee conectar.</span><span class="sxs-lookup"><span data-stu-id="6809f-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![crear la conexión con la cuenta de integración](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="6809f-123">Aquellas propiedades con un asterisco son obligatorias.</span><span class="sxs-lookup"><span data-stu-id="6809f-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="6809f-124">Propiedad</span><span class="sxs-lookup"><span data-stu-id="6809f-124">Property</span></span> | <span data-ttu-id="6809f-125">Detalles</span><span class="sxs-lookup"><span data-stu-id="6809f-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="6809f-126">Nombre de la conexión *</span><span class="sxs-lookup"><span data-stu-id="6809f-126">Connection Name *</span></span> |<span data-ttu-id="6809f-127">Escriba cualquier nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="6809f-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="6809f-128">Cuenta de integración*</span><span class="sxs-lookup"><span data-stu-id="6809f-128">Integration Account *</span></span> |<span data-ttu-id="6809f-129">Escriba un nombre para la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="6809f-129">Enter a name for your integration account.</span></span> <span data-ttu-id="6809f-130">Asegúrese de que la cuenta de integración y la aplicación lógica se encuentren en la misma ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="6809f-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="6809f-131">Cuando haya terminado, los detalles de la conexión deberían parecerse a este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="6809f-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="6809f-132">Para terminar de crear la conexión, elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6809f-132">To finish creating your connection, choose **Create**.</span></span>
   
    ![detalles de la conexión de integración](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="6809f-134">Una vez creada la conexión, como se muestra en este ejemplo, proporcione los detalles de los identificadores **AS2-From**, **AS2-To** como esté configurado en el contrato y de **Cuerpo**, que es la carga útil del mensaje.</span><span class="sxs-lookup"><span data-stu-id="6809f-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-To identifiers** as configured in your agreement, and **Body**, which is the message payload.</span></span>
   
    ![especificar los campos obligatorios](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="6809f-136">Detalles de codificador de AS2</span><span class="sxs-lookup"><span data-stu-id="6809f-136">AS2 encoder details</span></span>

<span data-ttu-id="6809f-137">El conector de codificación AS2 lleva a cabo estas tareas:</span><span class="sxs-lookup"><span data-stu-id="6809f-137">The Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="6809f-138">Aplica los encabezados AS2/HTTP.</span><span class="sxs-lookup"><span data-stu-id="6809f-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="6809f-139">Firma los mensajes salientes (en caso de haberse configurado).</span><span class="sxs-lookup"><span data-stu-id="6809f-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="6809f-140">Cifra los mensajes salientes (en caso de haberse configurado).</span><span class="sxs-lookup"><span data-stu-id="6809f-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="6809f-141">Comprime el mensaje (en caso de haberse configurado).</span><span class="sxs-lookup"><span data-stu-id="6809f-141">Compresses the message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="6809f-142">Ejemplo para probar</span><span class="sxs-lookup"><span data-stu-id="6809f-142">Try this sample</span></span>

<span data-ttu-id="6809f-143">Para intentar implementar una aplicación lógica totalmente operativa y conocer el escenario de ejemplo de AS2, consulte el artículo sobre [escenario y plantilla de aplicaciones lógicas de AS2](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="6809f-143">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="6809f-144">Visualización de Swagger</span><span class="sxs-lookup"><span data-stu-id="6809f-144">View the swagger</span></span>
<span data-ttu-id="6809f-145">Vea los [detalles de Swagger](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="6809f-145">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6809f-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6809f-146">Next steps</span></span>
[<span data-ttu-id="6809f-147">Más información sobre Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="6809f-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Información sobre Enterprise Integration Pack") 

