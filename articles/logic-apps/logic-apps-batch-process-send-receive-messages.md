---
title: "aaaBatch procesar mensajes como un grupo o una colección - Azure Logic Apps | Documentos de Microsoft"
description: "Envío y recepción de mensajes para el procesamiento por lotes en Logic Apps"
keywords: lote, proceso por lotes
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a><span data-ttu-id="1e716-104">Envío, recepción y procesamiento por lotes de mensajes en Logic Apps</span><span class="sxs-lookup"><span data-stu-id="1e716-104">Send, receive, and batch process messages in logic apps</span></span>

<span data-ttu-id="1e716-105">tooprocess mensajes en grupos, puede enviar datos elementos, o los mensajes, tooa *lote*y, a continuación, procesar los elementos como un lote.</span><span class="sxs-lookup"><span data-stu-id="1e716-105">tooprocess messages together in groups, you can send data items, or messages, tooa *batch*, and then process those items as a batch.</span></span> <span data-ttu-id="1e716-106">Este enfoque es útil cuando desea toomake seguro de elementos de datos se agrupan de forma específica y se procesan.</span><span class="sxs-lookup"><span data-stu-id="1e716-106">This approach is useful when you want toomake sure data items are grouped in a specific way and are processed together.</span></span> 

<span data-ttu-id="1e716-107">Puede crear aplicaciones de lógica que reciben elementos como un lote mediante el uso de hello **lote** desencadenador.</span><span class="sxs-lookup"><span data-stu-id="1e716-107">You can create logic apps that receive items as a batch by using hello **Batch** trigger.</span></span> <span data-ttu-id="1e716-108">A continuación, puede crear aplicaciones de lógica que envían elementos tooa lote mediante hello **lote** acción.</span><span class="sxs-lookup"><span data-stu-id="1e716-108">You can then create logic apps that send items tooa batch by using hello **Batch** action.</span></span>

<span data-ttu-id="1e716-109">Este tema muestra cómo puede compilar una solución de procesamiento por lotes mediante la realización de estas tareas:</span><span class="sxs-lookup"><span data-stu-id="1e716-109">This topic shows how you can build a batching solution by performing these tasks:</span></span> 

* <span data-ttu-id="1e716-110">[Cree una aplicación de lógica que reciba y recopile elementos como lote](#batch-receiver).</span><span class="sxs-lookup"><span data-stu-id="1e716-110">[Create a logic app that receives and collects items as a batch](#batch-receiver).</span></span> <span data-ttu-id="1e716-111">Esta aplicación de lógica de "receptor de lote" especifica toomeet de criterios de nombre y la versión del lote Hola antes de aplicación lógica de hello receptor libera y procesa los elementos.</span><span class="sxs-lookup"><span data-stu-id="1e716-111">This "batch receiver" logic app specifies hello batch name and release criteria toomeet before hello receiver logic app releases and processes items.</span></span> 

* <span data-ttu-id="1e716-112">[Crear una aplicación de lógica que envía el lote de elementos tooa](#batch-sender).</span><span class="sxs-lookup"><span data-stu-id="1e716-112">[Create a logic app that sends items tooa batch](#batch-sender).</span></span> <span data-ttu-id="1e716-113">Esta aplicación de lógica de "remitente de lote" especifica dónde toosend elementos, que deben ser una aplicación existente de lógica de receptor de lote.</span><span class="sxs-lookup"><span data-stu-id="1e716-113">This "batch sender" logic app specifies where toosend items, which must be an existing batch receiver logic app.</span></span> <span data-ttu-id="1e716-114">Puede especificar una clave única, como un número de cliente, demasiado "partition" o dividir por lotes de destino de hello en subconjuntos basándose en esa clave.</span><span class="sxs-lookup"><span data-stu-id="1e716-114">You can also specify a unique key, like a customer number, too"partition", or divide, hello target batch into subsets based on that key.</span></span> <span data-ttu-id="1e716-115">De este modo, todos los elementos con esa clave se recopilarán y procesarán juntos.</span><span class="sxs-lookup"><span data-stu-id="1e716-115">That way, all items with that key are collected and processed together.</span></span> 

## <a name="requirements"></a><span data-ttu-id="1e716-116">Requisitos</span><span class="sxs-lookup"><span data-stu-id="1e716-116">Requirements</span></span>

<span data-ttu-id="1e716-117">toofollow en este ejemplo, necesita estos elementos:</span><span class="sxs-lookup"><span data-stu-id="1e716-117">toofollow this example, you need these items:</span></span>

* <span data-ttu-id="1e716-118">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e716-118">An Azure subscription.</span></span> <span data-ttu-id="1e716-119">Si no tiene una suscripción, puede [comenzar con una cuenta de Azure gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="1e716-119">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="1e716-120">También puede [registrarse para obtener una suscripción de pago por uso](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="1e716-120">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="1e716-121">Conocimientos básicos sobre [cómo las aplicaciones lógicas toocreate](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="1e716-121">Basic knowledge about [how toocreate logic apps](../logic-apps/logic-apps-create-a-logic-app.md)</span></span> 

* <span data-ttu-id="1e716-122">Una cuenta de correo electrónico con cualquier [proveedor de correo electrónico compatible con Azure Logic Apps](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="1e716-122">An email account with any [email provider supported by Azure Logic Apps](../connectors/apis-list.md)</span></span>

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a><span data-ttu-id="1e716-123">Creación de aplicaciones lógicas que reciben mensajes como lote</span><span class="sxs-lookup"><span data-stu-id="1e716-123">Create logic apps that receive messages as a batch</span></span>

<span data-ttu-id="1e716-124">Para poder enviar lotes de mensajes tooa, primero debe crear una aplicación de la lógica de "receptor de lote" con hello **lote** desencadenador.</span><span class="sxs-lookup"><span data-stu-id="1e716-124">Before you can send messages tooa batch, you must first create a "batch receiver" logic app with hello **Batch** trigger.</span></span> <span data-ttu-id="1e716-125">De este modo, puede seleccionar esta aplicación de lógica de receptor, al crear una aplicación de lógica de remitente de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e716-125">That way, you can select this receiver logic app when you create hello sender logic app.</span></span> <span data-ttu-id="1e716-126">Para un receptor de hello, especifique el nombre del lote de hello, criterios de versión y otras opciones.</span><span class="sxs-lookup"><span data-stu-id="1e716-126">For hello receiver, you specify hello batch name, release criteria, and other settings.</span></span> 

<span data-ttu-id="1e716-127">Deben conocer las aplicaciones lógicas de remitente donde los elementos toosend, mientras que las aplicaciones lógicas de receptor no es necesario tooknow nada sobre remitentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e716-127">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="1e716-128">Hola [portal de Azure](https://portal.azure.com), cree una aplicación de lógica con este nombre: "BatchReceiver"</span><span class="sxs-lookup"><span data-stu-id="1e716-128">In hello [Azure portal](https://portal.azure.com), create a logic app with this name: "BatchReceiver"</span></span> 

2. <span data-ttu-id="1e716-129">En el Diseñador de aplicaciones de lógica, agregar hello **lote** desencadenador, que inicia el flujo de trabajo de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="1e716-129">In Logic Apps Designer, add hello **Batch** trigger, which starts your logic app workflow.</span></span> <span data-ttu-id="1e716-130">En el cuadro de búsqueda de hello, escriba "por lotes" como filtro.</span><span class="sxs-lookup"><span data-stu-id="1e716-130">In hello search box, enter "batch" as your filter.</span></span> <span data-ttu-id="1e716-131">Seleccione este desencadenador: **Batch: Mensajes de Batch**</span><span class="sxs-lookup"><span data-stu-id="1e716-131">Select this trigger: **Batch – Batch messages**</span></span>

   ![Agregar desencadenador de lotes](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. <span data-ttu-id="1e716-133">Proporcione un nombre para el lote de Hola y especificar los criterios para liberar el lote de hello, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1e716-133">Provide a name for hello batch, and specify criteria for releasing hello batch, for example:</span></span>

   * <span data-ttu-id="1e716-134">**Nombre de lote**: Hola nombre utilizado tooidentify Hola por lotes, que es "TestBatch" en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1e716-134">**Batch Name**: hello name used tooidentify hello batch, which is "TestBatch" in this example.</span></span>
   * <span data-ttu-id="1e716-135">**Número de mensajes**: Hola número de mensajes toohold como un lote antes de soltar el procesamiento, que es "5" en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1e716-135">**Message Count**: hello number of messages toohold as a batch before releasing for processing, which is "5" in this example.</span></span>

   ![Proporcionar detalles del desencadenador de lotes](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. <span data-ttu-id="1e716-137">Agregar otra acción que envía un correo electrónico cuando se activa el desencadenador de lote de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e716-137">Add another action that sends an email when hello batch trigger fires.</span></span> <span data-ttu-id="1e716-138">Cada lote de Hola de tiempo tiene cinco elementos, aplicación de lógica de hello envía un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="1e716-138">Each time hello batch has five items, hello logic app sends an email.</span></span>

   1. <span data-ttu-id="1e716-139">En el desencadenador de lote de hello, elija **+ nuevo paso** > **agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="1e716-139">Under hello batch trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="1e716-140">En el cuadro de búsqueda de hello, escriba "email" como filtro.</span><span class="sxs-lookup"><span data-stu-id="1e716-140">In hello search box, enter "email" as your filter.</span></span>
   <span data-ttu-id="1e716-141">En función de su proveedor de correo electrónico, seleccione un conector de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="1e716-141">Based on your email provider, select an email connector.</span></span>
   
      <span data-ttu-id="1e716-142">Por ejemplo, si tiene una cuenta profesional o educativa, seleccione Hola conector de Outlook de Office 365.</span><span class="sxs-lookup"><span data-stu-id="1e716-142">For example, if you have a work or school account, select hello Office 365 Outlook connector.</span></span> 
      <span data-ttu-id="1e716-143">Si tiene una cuenta de Gmail, seleccione el conector de Gmail de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e716-143">If you have a Gmail account, select hello Gmail connector.</span></span>

   3. <span data-ttu-id="1e716-144">Seleccione esta acción para el conector: **{*proveedor de correo electrónico*} - Enviar un correo electrónico**</span><span class="sxs-lookup"><span data-stu-id="1e716-144">Select this action for your connector: **{*email provider*} - Send an email**</span></span>

      <span data-ttu-id="1e716-145">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1e716-145">For example:</span></span>

      ![Seleccione la acción "Enviar un correo electrónico" para el proveedor de correo electrónico](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. <span data-ttu-id="1e716-147">Si anteriormente no creó una conexión para su proveedor de correo electrónico, proporcione sus credenciales de correo electrónico para la autenticación cuando se le soliciten.</span><span class="sxs-lookup"><span data-stu-id="1e716-147">If you didn't previously create a connection for your email provider, provide your email credentials for authentication when prompted.</span></span> <span data-ttu-id="1e716-148">Obtenga más información sobre la [autenticación de sus credenciales de correo electrónico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1e716-148">Learn more about [authenticating your email credentials](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

6. <span data-ttu-id="1e716-149">Establecer las propiedades de hello para la acción de Hola que acaba de agregar.</span><span class="sxs-lookup"><span data-stu-id="1e716-149">Set hello properties for hello action you just added.</span></span>

   * <span data-ttu-id="1e716-150">Hola **a** cuadro, escriba la dirección de correo electrónico del destinatario de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e716-150">In hello **To** box, enter hello recipient's email address.</span></span> 
   <span data-ttu-id="1e716-151">Para realizar pruebas, puede usar su propia dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="1e716-151">For testing purposes, you can use your own email address.</span></span>

   * <span data-ttu-id="1e716-152">Hola **asunto** cuadro cuando hello **contenido dinámico** aparece en la lista, seleccione hello **nombre de la partición** campo.</span><span class="sxs-lookup"><span data-stu-id="1e716-152">In hello **Subject** box, when hello **Dynamic content** list appears, select hello **Partition Name** field.</span></span>

     ![En lista de "Contenido dinámico" Hola, seleccione "Nombre de partición"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     <span data-ttu-id="1e716-154">En una sección posterior, puede especificar una clave de partición única que divide Hola por lotes de destino en lógica establece toowhere puede enviar mensajes.</span><span class="sxs-lookup"><span data-stu-id="1e716-154">In a later section, you can specify a unique partition key that divides hello target batch into logical sets toowhere you can send messages.</span></span> 
     <span data-ttu-id="1e716-155">Cada conjunto tiene un número único generado por la aplicación de lógica de hello remitente.</span><span class="sxs-lookup"><span data-stu-id="1e716-155">Each set has a unique number that's generated by hello sender logic app.</span></span> 
     <span data-ttu-id="1e716-156">Esta funcionalidad le permite usar un único lote con varios subconjuntos y definir cada subconjunto con nombre hello proporcionada por usted.</span><span class="sxs-lookup"><span data-stu-id="1e716-156">This capability lets you use a single batch with multiple subsets and define each subset with hello name that you provide.</span></span>

   * <span data-ttu-id="1e716-157">Hola **cuerpo** cuadro cuando hello **contenido dinámico** aparece en la lista, seleccione hello **Id. de mensaje** campo.</span><span class="sxs-lookup"><span data-stu-id="1e716-157">In hello **Body** box, when hello **Dynamic content** list appears, select hello **Message Id** field.</span></span>

     ![En "Cuerpo", seleccione "Id. del mensaje"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     <span data-ttu-id="1e716-159">Como entrada de hello para la acción de correo electrónico de envío de Hola es una matriz, Diseñador de hello agrega automáticamente un **para cada** trazo alrededor de hello **enviar un correo electrónico** acción.</span><span class="sxs-lookup"><span data-stu-id="1e716-159">Because hello input for hello send email action is an array, hello designer automatically adds a **For each** loop around hello **Send an email** action.</span></span> 
     <span data-ttu-id="1e716-160">Este bucle realiza la acción interna de hello en cada elemento de lote de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e716-160">This loop performs hello inner action on each item in hello batch.</span></span> 
     <span data-ttu-id="1e716-161">Por lo tanto, con elementos de toofive del conjunto Hola de desencadenador de lote, dispone de cinco mensajes de correo electrónico que se activa cada desencadenador de Hola de tiempo.</span><span class="sxs-lookup"><span data-stu-id="1e716-161">So, with hello batch trigger set toofive items, you get five emails each time hello trigger fires.</span></span>

7.  <span data-ttu-id="1e716-162">Ahora que ha creado una aplicación lógica receptora de lotes, guárdela.</span><span class="sxs-lookup"><span data-stu-id="1e716-162">Now that you created a batch receiver logic app, save your logic app.</span></span>

    ![Guardado de la aplicación lógica](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a><span data-ttu-id="1e716-164">Crear aplicaciones de lógica que envían mensajes tooa lote</span><span class="sxs-lookup"><span data-stu-id="1e716-164">Create logic apps that send messages tooa batch</span></span>

<span data-ttu-id="1e716-165">Ahora cree una o más aplicaciones de lógica que envían elementos toohello lote definido por la aplicación de lógica de receptor de hello.</span><span class="sxs-lookup"><span data-stu-id="1e716-165">Now create one or more logic apps that send items toohello batch defined by hello receiver logic app.</span></span> <span data-ttu-id="1e716-166">Para el remitente de hello, especificar aplicación lógica de receptor de Hola y nombre de lote, el contenido del mensaje y las opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="1e716-166">For hello sender, you specify hello receiver logic app and batch name, message content, and any other settings.</span></span> <span data-ttu-id="1e716-167">También puede proporcionar un lote de hello toodivide clave de partición única en elementos de toocollect de subconjuntos con esa clave.</span><span class="sxs-lookup"><span data-stu-id="1e716-167">You can optionally provide a unique partition key toodivide hello batch into subsets toocollect items with that key.</span></span>

<span data-ttu-id="1e716-168">Deben conocer las aplicaciones lógicas de remitente donde los elementos toosend, mientras que las aplicaciones lógicas de receptor no es necesario tooknow nada sobre remitentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e716-168">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="1e716-169">Cree otra aplicación lógica con este nombre: "BatchSender".</span><span class="sxs-lookup"><span data-stu-id="1e716-169">Create another logic app with this name: "BatchSender"</span></span>

   1. <span data-ttu-id="1e716-170">En el cuadro de búsqueda de hello, escriba "recurrence" como filtro.</span><span class="sxs-lookup"><span data-stu-id="1e716-170">In hello search box, enter "recurrence" as your filter.</span></span> 
   <span data-ttu-id="1e716-171">Seleccione este desencadenador: **Programación: Periodicidad**</span><span class="sxs-lookup"><span data-stu-id="1e716-171">Select this trigger: **Schedule - Recurrence**</span></span>

      ![Agregar desencadenador de Hola "Periodicidad de la programación"](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. <span data-ttu-id="1e716-173">Establezca frecuencia de Hola y la aplicación de lógica de intervalo toorun Hola remitente cada minuto.</span><span class="sxs-lookup"><span data-stu-id="1e716-173">Set hello frequency and interval toorun hello sender logic app every minute.</span></span>

      ![Establecer la frecuencia y el intervalo del desencadenador Periodicidad](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. <span data-ttu-id="1e716-175">Agregar un nuevo paso para enviar mensajes tooa lote.</span><span class="sxs-lookup"><span data-stu-id="1e716-175">Add a new step for sending messages tooa batch.</span></span>

   1. <span data-ttu-id="1e716-176">En el desencadenador de periodicidad de hello, elija **+ nuevo paso** > **agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="1e716-176">Under hello recurrence trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="1e716-177">En el cuadro de búsqueda de hello, escriba "por lotes" como filtro.</span><span class="sxs-lookup"><span data-stu-id="1e716-177">In hello search box, enter "batch" as your filter.</span></span> 

   3. <span data-ttu-id="1e716-178">Seleccione esta acción: **enviar mensajes toobatch: elija un flujo de trabajo de las aplicaciones lógicas con el desencadenador de lote**</span><span class="sxs-lookup"><span data-stu-id="1e716-178">Select this action: **Send messages toobatch – Choose a Logic Apps workflow with batch trigger**</span></span>

      ![Seleccione "Enviar mensajes toobatch"](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. <span data-ttu-id="1e716-180">Ahora seleccione la aplicación lógica "BatchReceiver" que creó anteriormente, que ahora aparece como una acción.</span><span class="sxs-lookup"><span data-stu-id="1e716-180">Now select your "BatchReceiver" logic app that you previously created, which now appears as an action.</span></span>

      ![Seleccionar aplicación lógica "receptora de lotes"](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > <span data-ttu-id="1e716-182">lista de Hello también muestra cualquier otra aplicación de lógica que tienen desencadenadores de lote.</span><span class="sxs-lookup"><span data-stu-id="1e716-182">hello list also shows any other logic apps that have batch triggers.</span></span>

3. <span data-ttu-id="1e716-183">Establecer las propiedades de lote de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e716-183">Set hello batch properties.</span></span>

   * <span data-ttu-id="1e716-184">**Nombre de lote**: nombre del lote Hola definido por la aplicación de lógica de receptor de hello, que es "TestBatch" en este ejemplo y se valida en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="1e716-184">**Batch Name**: hello batch name defined by hello receiver logic app, which is "TestBatch" in this example and is validated at runtime.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="1e716-185">Asegúrese de que no cambie el nombre del lote de hello, que debe coincidir con el nombre de lote de hello especificado por la aplicación de lógica de hello receptor.</span><span class="sxs-lookup"><span data-stu-id="1e716-185">Make sure that you don't change hello batch name, which must match hello batch name that's specified by hello receiver logic app.</span></span>
     > <span data-ttu-id="1e716-186">Cambiar nombre de lote de Hola hace que el remitente de hello toofail de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="1e716-186">Changing hello batch name causes hello sender logic app toofail.</span></span>

   * <span data-ttu-id="1e716-187">**Contenido del mensaje**: Hola contenido del mensaje que desea toosend.</span><span class="sxs-lookup"><span data-stu-id="1e716-187">**Message Content**: hello message content that you want toosend.</span></span> 
   <span data-ttu-id="1e716-188">En este ejemplo, agregue esta expresión que inserciones Hola fecha y hora actuales en el mensaje de bienvenida de contenido que enviar toohello lote:</span><span class="sxs-lookup"><span data-stu-id="1e716-188">For this example, add this expression that inserts hello current date and time into hello message content that you send toohello batch:</span></span>

     1. <span data-ttu-id="1e716-189">Cuando Hola **contenido dinámico** aparece en la lista, elija **expresión**.</span><span class="sxs-lookup"><span data-stu-id="1e716-189">When hello **Dynamic content** list appears, choose **Expression**.</span></span> 
     2. <span data-ttu-id="1e716-190">Escriba la expresión de hello **utcnow()**y elija **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1e716-190">Enter hello expression **utcnow()**, and choose **OK**.</span></span> 

        ![En "Contenido del mensaje", elija "Expresión".](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. <span data-ttu-id="1e716-193">Ahora debe configurar una partición para el lote de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e716-193">Now set up a partition for hello batch.</span></span> <span data-ttu-id="1e716-194">En la acción "BatchReceiver" Hola, elija **Mostrar opciones avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="1e716-194">In hello "BatchReceiver" action, choose **Show advanced options**.</span></span>

   * <span data-ttu-id="1e716-195">**Nombre de partición**: una toouse de clave de partición único opcional para dividir el lote de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e716-195">**Partition Name**: An optional unique partition key toouse for dividing hello target batch.</span></span> <span data-ttu-id="1e716-196">En este ejemplo, agregue una expresión que genera un número aleatorio entre uno y cinco.</span><span class="sxs-lookup"><span data-stu-id="1e716-196">For this example, add an expression that generates a random number between one and five.</span></span>
   
     1. <span data-ttu-id="1e716-197">Cuando Hola **contenido dinámico** aparece en la lista, elija **expresión**.</span><span class="sxs-lookup"><span data-stu-id="1e716-197">When hello **Dynamic content** list appears, choose **Expression**.</span></span>
     2. <span data-ttu-id="1e716-198">Escriba esta expresión: **rand(1,6)**</span><span class="sxs-lookup"><span data-stu-id="1e716-198">Enter this expression: **rand(1,6)**</span></span>

        ![Establecer una partición para el lote de destino](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        <span data-ttu-id="1e716-200">Esta función **rand** genera un número comprendido entre uno y cinco.</span><span class="sxs-lookup"><span data-stu-id="1e716-200">This **rand** function generates a number between one and five.</span></span> 
        <span data-ttu-id="1e716-201">Por tanto, va a dividir este lote en cinco particiones numeradas, que esta expresión establece dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="1e716-201">So you are dividing this batch into five numbered partitions, which this expression dynamically sets.</span></span>

   * <span data-ttu-id="1e716-202">**Id. de mensaje**: un identificador de mensaje opcional que es un GUID generado cuando está vacío.</span><span class="sxs-lookup"><span data-stu-id="1e716-202">**Message Id**: An optional message identifier and is a generated GUID when empty.</span></span> 
   <span data-ttu-id="1e716-203">En este ejemplo, deje este cuadro en blanco.</span><span class="sxs-lookup"><span data-stu-id="1e716-203">For this example, leave this box blank.</span></span>

5. <span data-ttu-id="1e716-204">Guarde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="1e716-204">Save your logic app.</span></span> <span data-ttu-id="1e716-205">La aplicación de la lógica de remitente parece ejemplo toothis similar:</span><span class="sxs-lookup"><span data-stu-id="1e716-205">Your sender logic app now looks similar toothis example:</span></span>

   ![Guardar la aplicación lógica remitente](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a><span data-ttu-id="1e716-207">Comprobación de las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="1e716-207">Test your logic apps</span></span>

<span data-ttu-id="1e716-208">tootest el procesamiento por lotes de la solución, deje las aplicaciones lógicas que se ejecuta durante unos minutos.</span><span class="sxs-lookup"><span data-stu-id="1e716-208">tootest your batching solution, leave your logic apps running for a few minutes.</span></span> <span data-ttu-id="1e716-209">Pronto, empezar a recibir mensajes de correo electrónico en los grupos de cinco, todo ello con hello misma clave de partición.</span><span class="sxs-lookup"><span data-stu-id="1e716-209">Soon, you start getting emails in groups of five, all with hello same partition key.</span></span>

<span data-ttu-id="1e716-210">La aplicación de la lógica de BatchSender ejecuta cada minuto, genera un número aleatorio entre uno y cinco y utiliza este número, generado como clave de partición de hello para el lote de destino de Hola dónde se envían los mensajes.</span><span class="sxs-lookup"><span data-stu-id="1e716-210">Your BatchSender logic app runs every minute, generates a random number between one and five, and uses this generated number as hello partition key for hello target batch where messages are sent.</span></span> <span data-ttu-id="1e716-211">Cada vez que el lote de hello tiene cinco elementos con hello misma clave de partición, la aplicación de la lógica de BatchReceiver se activa y envía el correo electrónico para cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="1e716-211">Each time hello batch has five items with hello same partition key, your BatchReceiver logic app fires and sends mail for each message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1e716-212">Cuando haya terminado de pruebas, asegúrese de que deshabilitar el envío de mensajes de Hola BatchSender lógica aplicación toostop y evitar la sobrecarga de la Bandeja de entrada.</span><span class="sxs-lookup"><span data-stu-id="1e716-212">When you're done testing, make sure that you disable hello BatchSender logic app toostop sending messages and avoid overloading your inbox.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e716-213">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1e716-213">Next steps</span></span>

* [<span data-ttu-id="1e716-214">Generar definiciones de aplicación lógica mediante el uso de JSON</span><span class="sxs-lookup"><span data-stu-id="1e716-214">Build on logic app definitions by using JSON</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="1e716-215">Cree una aplicación sin servidor en Visual Studio con Azure Logic Apps y Functions</span><span class="sxs-lookup"><span data-stu-id="1e716-215">Build a serverless app in Visual Studio with Azure Logic Apps and Functions</span></span>](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [<span data-ttu-id="1e716-216">Control de excepciones y registro de errores para aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="1e716-216">Exception handling and error logging for logic apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
