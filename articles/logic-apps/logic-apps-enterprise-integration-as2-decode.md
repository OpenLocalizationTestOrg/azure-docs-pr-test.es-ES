---
title: "Descodificación de mensajes AS2: Azure Logic Apps | Microsoft Docs"
description: Uso del descodificador AS2 en Enterprise Integration Pack para Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: a7920b2509fe368c6f7d55e17fe0bf0020c4562c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="6ea4a-103">Descodificación de mensajes AS2 para Azure Logic Apps con Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="6ea4a-103">Decode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span> 

<span data-ttu-id="6ea4a-104">Utilice el conector de descodificación de mensajes AS2 para garantizar la seguridad y confiabilidad al transmitir mensajes.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-104">To establish security and reliability while transmitting messages, use the Decode AS2 message connector.</span></span> <span data-ttu-id="6ea4a-105">Este conector proporciona firma digital, descifrado y confirmaciones a través de las notificaciones de disposición de mensajes (MDN).</span><span class="sxs-lookup"><span data-stu-id="6ea4a-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="6ea4a-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="6ea4a-106">Before you start</span></span>

<span data-ttu-id="6ea4a-107">Esto es lo que necesita:</span><span class="sxs-lookup"><span data-stu-id="6ea4a-107">Here's the items you need:</span></span>

* <span data-ttu-id="6ea4a-108">Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="6ea4a-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="6ea4a-109">Una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md) que ya esté definida y asociada a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="6ea4a-110">Debe tener una cuenta de integración para usar el conector de descodificación de mensajes AS2.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-110">You must have an integration account to use the Decode AS2 message connector.</span></span>
* <span data-ttu-id="6ea4a-111">Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="6ea4a-112">Un [contrato AS2](logic-apps-enterprise-integration-as2.md) ya definido en la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="6ea4a-113">Descodificación de mensajes AS2</span><span class="sxs-lookup"><span data-stu-id="6ea4a-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="6ea4a-114">[Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6ea4a-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="6ea4a-115">El conector de descodificación de mensajes AS2 no tiene desencadenadores, por lo que debe agregar uno para iniciar la aplicación lógica, por ejemplo, un desencadenador de solicitud.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-115">The Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="6ea4a-116">En el Diseñador de aplicaciones lógicas, agregue un desencadenador y una acción a la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="6ea4a-117">En el cuadro de búsqueda, escriba "AS2" para el filtro.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="6ea4a-118">Seleccione **AS2 – Decode AS2 Message** (AS2: descodificación de mensajes AS2).</span><span class="sxs-lookup"><span data-stu-id="6ea4a-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    ![Búsqueda de "AS2"](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="6ea4a-120">Si no había creado ninguna conexión a la cuenta de integración, se le pedirá que lo haga ahora.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="6ea4a-121">Asigne un nombre a la conexión y seleccione la cuenta de integración que desee conectar.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![Crear conexión de integración](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="6ea4a-123">Aquellas propiedades con un asterisco son obligatorias.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="6ea4a-124">Propiedad</span><span class="sxs-lookup"><span data-stu-id="6ea4a-124">Property</span></span> | <span data-ttu-id="6ea4a-125">Detalles</span><span class="sxs-lookup"><span data-stu-id="6ea4a-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="6ea4a-126">Nombre de la conexión *</span><span class="sxs-lookup"><span data-stu-id="6ea4a-126">Connection Name *</span></span> |<span data-ttu-id="6ea4a-127">Escriba cualquier nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="6ea4a-128">Cuenta de integración*</span><span class="sxs-lookup"><span data-stu-id="6ea4a-128">Integration Account *</span></span> |<span data-ttu-id="6ea4a-129">Escriba un nombre para la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-129">Enter a name for your integration account.</span></span> <span data-ttu-id="6ea4a-130">Asegúrese de que la cuenta de integración y la aplicación lógica se encuentren en la misma ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="6ea4a-131">Cuando haya terminado, los detalles de la conexión deberían parecerse a este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="6ea4a-132">Para terminar de crear la conexión, elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-132">To finish creating your connection, choose **Create**.</span></span>

    ![detalles de la conexión de integración](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="6ea4a-134">Una vez creada la conexión, como se muestra en este ejemplo, seleccione **Cuerpo** y **Encabezados** de las salidas de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-134">After your connection is created, as shown in this example, select **Body** and **Headers** from the Request outputs.</span></span>
   
    ![conexión de integración creada](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="6ea4a-136">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6ea4a-136">For example:</span></span>

    ![Seleccione el cuerpo y los encabezados de las salidas de la solicitud](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="6ea4a-138">Detalles de descodificador de AS2</span><span class="sxs-lookup"><span data-stu-id="6ea4a-138">AS2 decoder details</span></span>

<span data-ttu-id="6ea4a-139">El conector de descodificación AS2 lleva a cabo estas tareas:</span><span class="sxs-lookup"><span data-stu-id="6ea4a-139">The Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="6ea4a-140">Procesa encabezados AS2/HTTP.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="6ea4a-141">Comprueba la firma (si la opción está configurada).</span><span class="sxs-lookup"><span data-stu-id="6ea4a-141">Verifies the signature (if configured)</span></span>
* <span data-ttu-id="6ea4a-142">Descifra los mensajes (si la opción está configurada).</span><span class="sxs-lookup"><span data-stu-id="6ea4a-142">Decrypts the messages (if configured)</span></span>
* <span data-ttu-id="6ea4a-143">Descomprime el mensaje (si la opción está configurada).</span><span class="sxs-lookup"><span data-stu-id="6ea4a-143">Decompresses the message (if configured)</span></span>
* <span data-ttu-id="6ea4a-144">Reconcilia un MDN recibido con el mensaje de salida original.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-144">Reconciles a received MDN with the original outbound message</span></span>
* <span data-ttu-id="6ea4a-145">Actualiza y correlaciona registros en la base de datos sin repudio.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-145">Updates and correlates records in the non-repudiation database</span></span>
* <span data-ttu-id="6ea4a-146">Escribe registros para los informes de estado de AS2.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="6ea4a-147">El contenido de la carga útil de salida está codificado en base64.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-147">The output payload contents are base64 encoded</span></span>
* <span data-ttu-id="6ea4a-148">Determina si se requiere un MDN y si este debe ser sincrónico o asincrónico en función de la configuración del acuerdo AS2.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-148">Determines whether an MDN is required, and whether the MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="6ea4a-149">Genera un MDN sincrónico o asincrónico (en función de las configuraciones del acuerdo).</span><span class="sxs-lookup"><span data-stu-id="6ea4a-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="6ea4a-150">Establece las propiedades y los token de correlación en el MDN.</span><span class="sxs-lookup"><span data-stu-id="6ea4a-150">Sets the correlation tokens and properties on the MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="6ea4a-151">Ejemplo para probar</span><span class="sxs-lookup"><span data-stu-id="6ea4a-151">Try this sample</span></span>

<span data-ttu-id="6ea4a-152">Para intentar implementar una aplicación lógica totalmente operativa y conocer el escenario de ejemplo de AS2, consulte el artículo sobre [escenario y plantilla de aplicaciones lógicas de AS2](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="6ea4a-152">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="6ea4a-153">Visualización de Swagger</span><span class="sxs-lookup"><span data-stu-id="6ea4a-153">View the swagger</span></span>
<span data-ttu-id="6ea4a-154">Vea los [detalles de Swagger](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="6ea4a-154">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6ea4a-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6ea4a-155">Next steps</span></span>
[<span data-ttu-id="6ea4a-156">Más información acerca de Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="6ea4a-156">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 

