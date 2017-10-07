---
title: mensajes de AS2 aaaDecode - Azure Logic Apps | Documentos de Microsoft
description: "¿Cómo toouse Hola descodificador AS2 en hello paquete de integración empresarial para las aplicaciones lógicas de Azure"
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
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="3498f-103">Descodificar mensajes AS2 para las aplicaciones lógicas de Azure con hello paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="3498f-103">Decode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span> 

<span data-ttu-id="3498f-104">tooestablish seguridad y confiabilidad al transmitir los mensajes, utilice el conector de mensaje de AS2 descodificar de Hola.</span><span class="sxs-lookup"><span data-stu-id="3498f-104">tooestablish security and reliability while transmitting messages, use hello Decode AS2 message connector.</span></span> <span data-ttu-id="3498f-105">Este conector proporciona firma digital, descifrado y confirmaciones a través de las notificaciones de disposición de mensajes (MDN).</span><span class="sxs-lookup"><span data-stu-id="3498f-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="3498f-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="3498f-106">Before you start</span></span>

<span data-ttu-id="3498f-107">Aquí es elementos de Hola que necesita:</span><span class="sxs-lookup"><span data-stu-id="3498f-107">Here's hello items you need:</span></span>

* <span data-ttu-id="3498f-108">Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="3498f-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="3498f-109">Una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md) que ya esté definida y asociada a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3498f-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="3498f-110">Debe tener un conector de mensaje integración cuenta toouse Hola descodificar AS2.</span><span class="sxs-lookup"><span data-stu-id="3498f-110">You must have an integration account toouse hello Decode AS2 message connector.</span></span>
* <span data-ttu-id="3498f-111">Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="3498f-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="3498f-112">Un [contrato AS2](logic-apps-enterprise-integration-as2.md) ya definido en la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="3498f-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="3498f-113">Descodificación de mensajes AS2</span><span class="sxs-lookup"><span data-stu-id="3498f-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="3498f-114">[Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3498f-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="3498f-115">Conector de mensaje de Hola AS2 descodificar no tiene desencadenadores, por lo que debe agregar un desencadenador para iniciar la aplicación lógica, como un desencadenador de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="3498f-115">hello Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="3498f-116">Hola diseñador la lógica de aplicación, agregar un desencadenador y, a continuación, agregar una aplicación de lógica de tooyour de acción.</span><span class="sxs-lookup"><span data-stu-id="3498f-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="3498f-117">En el cuadro de búsqueda de hello, escriba "AS2" para el filtro.</span><span class="sxs-lookup"><span data-stu-id="3498f-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="3498f-118">Seleccione **AS2 – Decode AS2 Message** (AS2: descodificación de mensajes AS2).</span><span class="sxs-lookup"><span data-stu-id="3498f-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    ![Búsqueda de "AS2"](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="3498f-120">Si previamente no creó ninguna conexión de cuenta de integración de tooyour, se te pedirá toocreate ahora esa conexión.</span><span class="sxs-lookup"><span data-stu-id="3498f-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="3498f-121">Nombre de la conexión y seleccione cuenta de integración de Hola que desea tooconnect.</span><span class="sxs-lookup"><span data-stu-id="3498f-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![Crear conexión de integración](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="3498f-123">Aquellas propiedades con un asterisco son obligatorias.</span><span class="sxs-lookup"><span data-stu-id="3498f-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="3498f-124">Propiedad</span><span class="sxs-lookup"><span data-stu-id="3498f-124">Property</span></span> | <span data-ttu-id="3498f-125">Detalles</span><span class="sxs-lookup"><span data-stu-id="3498f-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="3498f-126">Nombre de la conexión *</span><span class="sxs-lookup"><span data-stu-id="3498f-126">Connection Name *</span></span> |<span data-ttu-id="3498f-127">Escriba cualquier nombre para la conexión.</span><span class="sxs-lookup"><span data-stu-id="3498f-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="3498f-128">Cuenta de integración*</span><span class="sxs-lookup"><span data-stu-id="3498f-128">Integration Account *</span></span> |<span data-ttu-id="3498f-129">Escriba un nombre para la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="3498f-129">Enter a name for your integration account.</span></span> <span data-ttu-id="3498f-130">Asegúrese de que la aplicación de cuenta y la lógica de integración están en hello misma ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="3498f-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="3498f-131">Cuando haya terminado, los detalles de la conexión deben tener un aspecto similar ejemplo toothis.</span><span class="sxs-lookup"><span data-stu-id="3498f-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="3498f-132">toofinish crear la conexión, elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="3498f-132">toofinish creating your connection, choose **Create**.</span></span>

    ![detalles de la conexión de integración](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="3498f-134">Una vez creada la conexión, como se muestra en este ejemplo, seleccione **cuerpo** y **encabezados** de hello solicitar salidas.</span><span class="sxs-lookup"><span data-stu-id="3498f-134">After your connection is created, as shown in this example, select **Body** and **Headers** from hello Request outputs.</span></span>
   
    ![conexión de integración creada](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="3498f-136">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3498f-136">For example:</span></span>

    ![Seleccione el cuerpo y los encabezados de las salidas de la solicitud](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="3498f-138">Detalles de descodificador de AS2</span><span class="sxs-lookup"><span data-stu-id="3498f-138">AS2 decoder details</span></span>

<span data-ttu-id="3498f-139">Hola descodificar AS2 conector lleva a cabo estas tareas:</span><span class="sxs-lookup"><span data-stu-id="3498f-139">hello Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="3498f-140">Procesa encabezados AS2/HTTP.</span><span class="sxs-lookup"><span data-stu-id="3498f-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="3498f-141">Comprueba la firma de hello (si está configurado)</span><span class="sxs-lookup"><span data-stu-id="3498f-141">Verifies hello signature (if configured)</span></span>
* <span data-ttu-id="3498f-142">Descifra los mensajes de saludo (si está configurado)</span><span class="sxs-lookup"><span data-stu-id="3498f-142">Decrypts hello messages (if configured)</span></span>
* <span data-ttu-id="3498f-143">Descomprime el mensaje de bienvenida (si está configurado)</span><span class="sxs-lookup"><span data-stu-id="3498f-143">Decompresses hello message (if configured)</span></span>
* <span data-ttu-id="3498f-144">Reconcilia un MDN recibido con el mensaje de salida original Hola</span><span class="sxs-lookup"><span data-stu-id="3498f-144">Reconciles a received MDN with hello original outbound message</span></span>
* <span data-ttu-id="3498f-145">Actualiza y correlaciona registros en la base de datos de hello sin repudio</span><span class="sxs-lookup"><span data-stu-id="3498f-145">Updates and correlates records in hello non-repudiation database</span></span>
* <span data-ttu-id="3498f-146">Escribe registros para los informes de estado de AS2.</span><span class="sxs-lookup"><span data-stu-id="3498f-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="3498f-147">contenido de carga de salida de Hello está codificados con base64</span><span class="sxs-lookup"><span data-stu-id="3498f-147">hello output payload contents are base64 encoded</span></span>
* <span data-ttu-id="3498f-148">Determina si es necesario, un MDN y si Hola MDN debe ser sincrónica o asincrónicas basados en configuración de acuerdo AS2</span><span class="sxs-lookup"><span data-stu-id="3498f-148">Determines whether an MDN is required, and whether hello MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="3498f-149">Genera un MDN sincrónico o asincrónico (en función de las configuraciones del acuerdo).</span><span class="sxs-lookup"><span data-stu-id="3498f-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="3498f-150">Establece propiedades y los tokens de correlación de hello en hello MDN</span><span class="sxs-lookup"><span data-stu-id="3498f-150">Sets hello correlation tokens and properties on hello MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="3498f-151">Ejemplo para probar</span><span class="sxs-lookup"><span data-stu-id="3498f-151">Try this sample</span></span>

<span data-ttu-id="3498f-152">tootry implementar un escenario de AS2 lógica totalmente operativo ejemplo y la aplicación, vea hello [AS2 plantilla de aplicación lógica y escenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="3498f-152">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="3498f-153">Swagger de hello de vista</span><span class="sxs-lookup"><span data-stu-id="3498f-153">View hello swagger</span></span>
<span data-ttu-id="3498f-154">Vea hello [swagger detalles](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="3498f-154">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3498f-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3498f-155">Next steps</span></span>
[<span data-ttu-id="3498f-156">Obtener más información sobre Hola paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="3498f-156">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 

