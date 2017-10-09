---
title: mensajes de AS2 aaaEncode - Azure Logic Apps | Documentos de Microsoft
description: "¿Cómo toouse Hola codificador AS2 de hello paquete de integración empresarial para las aplicaciones lógicas de Azure"
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
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="2b9bf-103">Codificar los mensajes de AS2 para las aplicaciones lógicas de Azure con hello paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="2b9bf-103">Encode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="2b9bf-104">tooestablish seguridad y confiabilidad al transmitir los mensajes, utilice conector de mensaje de Hola codificar AS2.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-104">tooestablish security and reliability while transmitting messages, use hello Encode AS2 message connector.</span></span> <span data-ttu-id="2b9bf-105">Este conector proporciona firma digital, cifrado y confirmaciones a través de notificaciones de disposición de mensaje (MDN), lo que conduce también toosupport para sin repudio.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads toosupport for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="2b9bf-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="2b9bf-106">Before you start</span></span>

<span data-ttu-id="2b9bf-107">Aquí es elementos de Hola que necesita:</span><span class="sxs-lookup"><span data-stu-id="2b9bf-107">Here's hello items you need:</span></span>

* <span data-ttu-id="2b9bf-108">Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="2b9bf-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="2b9bf-109">Una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md) que ya esté definida y asociada a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="2b9bf-110">Debe tener un conector integración cuenta toouse Hola AS2 codificar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-110">You must have an integration account toouse hello Encode AS2 message connector.</span></span>
* <span data-ttu-id="2b9bf-111">Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="2b9bf-112">Un [contrato AS2](logic-apps-enterprise-integration-as2.md) ya definido en la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="2b9bf-113">Codificación de mensajes AS2</span><span class="sxs-lookup"><span data-stu-id="2b9bf-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="2b9bf-114">[Creación de una aplicación lógica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2b9bf-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="2b9bf-115">Conector de mensaje de Hola codificar AS2 no tiene desencadenadores, por lo que debe agregar un desencadenador para iniciar la aplicación lógica, como un desencadenador de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-115">hello Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="2b9bf-116">Hola diseñador la lógica de aplicación, agregar un desencadenador y, a continuación, agregar una aplicación de lógica de tooyour de acción.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="2b9bf-117">En el cuadro de búsqueda de hello, escriba "AS2" para el filtro.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="2b9bf-118">Seleccione **AS2 – Encode AS2 Message** (AS2: codificación de mensajes AS2).</span><span class="sxs-lookup"><span data-stu-id="2b9bf-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    ![Búsqueda de "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="2b9bf-120">Si previamente no creó ninguna conexión de cuenta de integración de tooyour, se te pedirá toocreate ahora esa conexión.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="2b9bf-121">Nombre de la conexión y seleccione cuenta de integración de Hola que desea tooconnect.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![Crear cuenta de conexión de toointegration](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="2b9bf-123">Aquellas propiedades con un asterisco son obligatorias.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="2b9bf-124">Propiedad</span><span class="sxs-lookup"><span data-stu-id="2b9bf-124">Property</span></span> | <span data-ttu-id="2b9bf-125">Detalles</span><span class="sxs-lookup"><span data-stu-id="2b9bf-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="2b9bf-126">Nombre de la conexión *</span><span class="sxs-lookup"><span data-stu-id="2b9bf-126">Connection Name *</span></span> |<span data-ttu-id="2b9bf-127">Escriba cualquier nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="2b9bf-128">Cuenta de integración*</span><span class="sxs-lookup"><span data-stu-id="2b9bf-128">Integration Account *</span></span> |<span data-ttu-id="2b9bf-129">Escriba un nombre para la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-129">Enter a name for your integration account.</span></span> <span data-ttu-id="2b9bf-130">Asegúrese de que la aplicación de cuenta y la lógica de integración están en hello misma ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="2b9bf-131">Cuando haya terminado, los detalles de la conexión deben tener un aspecto similar ejemplo toothis.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="2b9bf-132">toofinish crear la conexión, elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![detalles de la conexión de integración](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="2b9bf-134">Una vez creada la conexión, como se muestra en este ejemplo, proporcione los detalles de **AS2-de**, **AS2 tooidentifiers** como está configurado en el acuerdo, y **cuerpo**, que es carga del mensaje Hola.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-tooidentifiers** as configured in your agreement, and **Body**, which is hello message payload.</span></span>
   
    ![especificar los campos obligatorios](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="2b9bf-136">Detalles de codificador de AS2</span><span class="sxs-lookup"><span data-stu-id="2b9bf-136">AS2 encoder details</span></span>

<span data-ttu-id="2b9bf-137">Hola codificar AS2 conector lleva a cabo estas tareas:</span><span class="sxs-lookup"><span data-stu-id="2b9bf-137">hello Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="2b9bf-138">Aplica los encabezados AS2/HTTP.</span><span class="sxs-lookup"><span data-stu-id="2b9bf-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="2b9bf-139">Firma los mensajes salientes (en caso de haberse configurado).</span><span class="sxs-lookup"><span data-stu-id="2b9bf-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="2b9bf-140">Cifra los mensajes salientes (en caso de haberse configurado).</span><span class="sxs-lookup"><span data-stu-id="2b9bf-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="2b9bf-141">Comprime el mensaje de bienvenida (si está configurado)</span><span class="sxs-lookup"><span data-stu-id="2b9bf-141">Compresses hello message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="2b9bf-142">Ejemplo para probar</span><span class="sxs-lookup"><span data-stu-id="2b9bf-142">Try this sample</span></span>

<span data-ttu-id="2b9bf-143">tootry implementar un escenario de AS2 lógica totalmente operativo ejemplo y la aplicación, vea hello [AS2 plantilla de aplicación lógica y escenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="2b9bf-143">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="2b9bf-144">Swagger de hello de vista</span><span class="sxs-lookup"><span data-stu-id="2b9bf-144">View hello swagger</span></span>
<span data-ttu-id="2b9bf-145">Vea hello [swagger detalles](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="2b9bf-145">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2b9bf-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2b9bf-146">Next steps</span></span>
[<span data-ttu-id="2b9bf-147">Obtener más información sobre Hola paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="2b9bf-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial") 

