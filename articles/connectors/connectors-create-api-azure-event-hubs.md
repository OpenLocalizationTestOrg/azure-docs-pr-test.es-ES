---
title: "aaaSet el monitor de eventos con los concentradores de eventos de Azure para las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Supervisar eventos de tooreceive de flujos de datos y enviar eventos para las aplicaciones lógicas de Azure con los concentradores de eventos de Azure"
services: logic-apps
keywords: "flujo de datos, supervisión de eventos, centros de eventos"
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a><span data-ttu-id="cf18a-104">Supervisar, recibir y enviar eventos con el conector de los centros de eventos de Hola</span><span class="sxs-lookup"><span data-stu-id="cf18a-104">Monitor, receive, and send events with hello Event Hubs connector</span></span>

<span data-ttu-id="cf18a-105">tooset un monitor de eventos para que pueda detectar eventos, eventos de recepción y enviar eventos, la aplicación lógica conectarse tooan [concentrador de eventos de Azure](https://azure.microsoft.com/services/event-hubs) desde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="cf18a-105">tooset up an event monitor so that your logic app can detect events, receive events, and send events, connect tooan [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="cf18a-106">Obtenga más información acerca de los [Centros de eventos de Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="cf18a-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="cf18a-107">Requisitos</span><span class="sxs-lookup"><span data-stu-id="cf18a-107">Requirements</span></span>

* <span data-ttu-id="cf18a-108">Tendrá que toohave una [concentrador de eventos y espacio de nombres de los centros de eventos](../event-hubs/event-hubs-create.md) en Azure.</span><span class="sxs-lookup"><span data-stu-id="cf18a-108">You have toohave an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="cf18a-109">Obtenga información acerca de [cómo toocreate un espacio de nombres de los centros de eventos y el centro de eventos](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="cf18a-109">Learn [how toocreate an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="cf18a-110">toouse [cualquier conector](https://docs.microsoft.com/azure/connectors/apis-list) en la aplicación lógica, tiene toocreate una aplicación lógica en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="cf18a-110">toouse [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have toocreate a logic app first.</span></span> <span data-ttu-id="cf18a-111">Obtenga información acerca de [cómo una aplicación de la lógica de toocreate](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="cf18a-111">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a><span data-ttu-id="cf18a-112">Comprobar los permisos del espacio de nombres de los centros de eventos y buscar la cadena de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="cf18a-112">Check Event Hubs namespace permissions and find hello connection string</span></span>

<span data-ttu-id="cf18a-113">Para su tooaccess de aplicación lógica de cualquier servicio, tendrá que toocreate una [ *conexión* ](./connectors-overview.md) entre su lógica hello y aplicación de servicio, si no lo ha hecho ya.</span><span class="sxs-lookup"><span data-stu-id="cf18a-113">For your logic app tooaccess any service, you have toocreate a [*connection*](./connectors-overview.md) between your logic app and hello service, if you haven't already.</span></span> <span data-ttu-id="cf18a-114">Esta conexión se autoriza a los datos de tooaccess de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="cf18a-114">This connection authorizes your logic app tooaccess data.</span></span>
<span data-ttu-id="cf18a-115">Para su tooaccess de aplicación lógica el centro de eventos, deberá toohave **administrar** permisos y la cadena de conexión de hello para el espacio de nombres de los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="cf18a-115">For your logic app tooaccess your Event Hub, you have toohave **Manage** permissions and hello connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="cf18a-116">toocheck sus permisos y la cadena de conexión de get hello, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="cf18a-116">toocheck your permissions and get hello connection string, follow these steps.</span></span>

1.  <span data-ttu-id="cf18a-117">Inicie sesión en toohello [portal de Azure](https://portal.azure.com "portal de Azure").</span><span class="sxs-lookup"><span data-stu-id="cf18a-117">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="cf18a-118">Vaya a los centros de eventos de tooyour *espacio de nombres*, no Hola centro de eventos específicos.</span><span class="sxs-lookup"><span data-stu-id="cf18a-118">Go tooyour Event Hubs *namespace*, not hello specific Event Hub.</span></span> <span data-ttu-id="cf18a-119">En la hoja de espacio de nombres de hello, en **configuración**, elija **directivas de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="cf18a-119">On hello namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="cf18a-120">En **Notificaciones**, compruebe que tenga permisos de **Administrador** para ese espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="cf18a-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![Administrar los permisos del espacio de nombres del Event Hub](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="cf18a-122">cadena de conexión de hello toocopy de espacio de nombres de los centros de eventos de hello, elija **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="cf18a-122">toocopy hello connection string for hello Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="cf18a-123">Siguiente tooyour principal clave de cadena de conexión, elija el botón Copiar de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf18a-123">Next tooyour primary key connection string, choose hello copy button.</span></span>

    ![Copie la cadena de conexión del espacio de nombres de los Event Hubs](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="cf18a-125">tooconfirm si la cadena de conexión está asociada con el espacio de nombres de los centros de eventos o con un concentrador de eventos específicos, comprobar la cadena de conexión de Hola Hola `EntityPath` parámetro.</span><span class="sxs-lookup"><span data-stu-id="cf18a-125">tooconfirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check hello connection string for hello `EntityPath` parameter.</span></span> <span data-ttu-id="cf18a-126">Si encuentra este parámetro, cadena de conexión de hello es para un centro de eventos específicos "entidad" y no es Hola cadena correcta toouse con la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="cf18a-126">If you find this parameter, hello connection string is for a specific Event Hub "entity", and is not hello correct string toouse with your logic app.</span></span>

4.  <span data-ttu-id="cf18a-127">Ahora cuando se le pide credenciales después de agregar una aplicación centros de eventos desencadenador o acción tooyour lógica, puede conectar el espacio de nombres de tooyour centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="cf18a-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action tooyour logic app, you can connect tooyour Event Hubs namespace.</span></span> <span data-ttu-id="cf18a-128">Asigne un nombre a la conexión, escriba la cadena de conexión de Hola que ha copiado y elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="cf18a-128">Give your connection a name, enter hello connection string that you copied, and choose **Create**.</span></span>

    ![Ingrese la cadena de conexión para el espacio de nombres de los Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="cf18a-130">Después de crear la conexión, nombre de la conexión de hello debe aparecer en el desencadenador de centros de eventos de Hola o acción.</span><span class="sxs-lookup"><span data-stu-id="cf18a-130">After you create your connection, hello connection name should appear in hello Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="cf18a-131">A continuación, puede continuar con Hola otros pasos de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="cf18a-131">You can then continue with hello other steps in your logic app.</span></span>

    ![Conexión del espacio de nombres de los Event Hubs creada](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="cf18a-133">Iniciar el flujo de trabajo cuando el Event Hub recibe eventos nuevos</span><span class="sxs-lookup"><span data-stu-id="cf18a-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="cf18a-134">Un [*desencadenador*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) es un evento que inicia un flujo de trabajo en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="cf18a-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="cf18a-135">Para iniciar un flujo de trabajo cuando se envían eventos nuevos tooyour concentrador de eventos, siga estos pasos para agregar el desencadenador de Hola que detecta este evento.</span><span class="sxs-lookup"><span data-stu-id="cf18a-135">To start a workflow when new events are sent tooyour Event Hub, follow these steps for adding hello trigger that detects this event.</span></span>

1.  <span data-ttu-id="cf18a-136">Hola [portal de Azure](https://portal.azure.com "portal de Azure"), vaya tooyour la aplicación lógica existente o cree una aplicación de lógica en blanco.</span><span class="sxs-lookup"><span data-stu-id="cf18a-136">In hello [Azure portal](https://portal.azure.com "Azure portal"), go tooyour existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="cf18a-137">En cuadro de búsqueda de Hola para hello diseñador la lógica de aplicación, escriba `event hubs` para el filtro.</span><span class="sxs-lookup"><span data-stu-id="cf18a-137">In hello search box for hello Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="cf18a-138">Seleccione este desencadenador: **Cuando los eventos estén disponibles en el Event Hub**</span><span class="sxs-lookup"><span data-stu-id="cf18a-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![Seleccione el desencadenador para cuando el Event Hub reciba eventos nuevos](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="cf18a-140">Si aún no tiene un espacio de nombres de los centros de eventos de tooyour de conexión, se te pedirá toocreate ahora esta conexión.</span><span class="sxs-lookup"><span data-stu-id="cf18a-140">If you don't already have a connection tooyour Event Hubs namespace, you're prompted toocreate this connection now.</span></span> <span data-ttu-id="cf18a-141">Asigne un nombre a la conexión y escriba la cadena de conexión de hello para el espacio de nombres de los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="cf18a-141">Give your connection a name, and enter hello connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="cf18a-142">Si es necesario, obtenga información acerca de [cómo toofind la cadena de conexión](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="cf18a-142">If necessary, learn [how toofind your connection string](#permissions-connection-string).</span></span>

    ![Ingrese la cadena de conexión para el espacio de nombres de los Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="cf18a-144">Después de crear la conexión de hello, Hola configuración de hello **cuando un evento en disponibles en un centro de eventos** aparecen de desencadenador.</span><span class="sxs-lookup"><span data-stu-id="cf18a-144">After you create hello connection, hello settings for hello **When an event in available in an Event Hub** trigger appear.</span></span>

    ![Configuración del desencadenador para cuando el Event Hub reciba eventos nuevos](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="cf18a-146">Escriba o seleccione el nombre Hola Hola concentrador de eventos que desea toomonitor.</span><span class="sxs-lookup"><span data-stu-id="cf18a-146">Enter or select hello name for hello Event Hub that you want toomonitor.</span></span> <span data-ttu-id="cf18a-147">Seleccione la frecuencia de Hola y de intervalo para la frecuencia con la que desea que toocheck Hola concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="cf18a-147">Select hello frequency and interval for how often you want toocheck hello Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="cf18a-148">toooptionally seleccionar un grupo de consumidores para leer los eventos, elija **Mostrar opciones avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="cf18a-148">toooptionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![Especificar Event Hub o grupo de consumidores](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="cf18a-150">Ya ha configurado un desencadenador toostart un flujo de trabajo para la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="cf18a-150">You've now set up a trigger toostart a workflow for your logic app.</span></span> 
    <span data-ttu-id="cf18a-151">La aplicación lógica comprueba Hola especificado en función de la programación de Hola que establezca el concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="cf18a-151">Your logic app checks hello specified Event Hub based on hello schedule that you set.</span></span> 
    <span data-ttu-id="cf18a-152">Si la aplicación busca nuevos eventos de hello concentrador de eventos, el desencadenador de hello ejecuta otras acciones o desencadenadores en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="cf18a-152">If your app finds new events in hello Event Hub, hello trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a><span data-ttu-id="cf18a-153">Enviar eventos tooyour concentrador de eventos desde la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="cf18a-153">Send events tooyour Event Hub from your logic app</span></span>

<span data-ttu-id="cf18a-154">Una [*acción*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) es una tarea realizada por el flujo de trabajo de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="cf18a-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="cf18a-155">Después de agregar una aplicación de lógica de desencadenador tooyour, puede agregar un operaciones tooperform de acción con los datos generados por este desencadenador.</span><span class="sxs-lookup"><span data-stu-id="cf18a-155">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="cf18a-156">toosend un tooyour de evento concentrador de eventos de la aplicación lógica, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="cf18a-156">toosend an event tooyour Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="cf18a-157">En el Diseñador de aplicaciones lógicas, bajo el desencadenador de la aplicación lógica, elija **Nuevo paso** > **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="cf18a-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    ![Haga clic en "Nuevo paso" y en "Agregar una acción"](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="cf18a-159">Ahora puede buscar y seleccionar un tooperform de acción.</span><span class="sxs-lookup"><span data-stu-id="cf18a-159">Now you can find and select an action tooperform.</span></span> 
    <span data-ttu-id="cf18a-160">Aunque puede seleccionar cualquier acción, en este ejemplo, queremos eventos de toosend de acción de hello centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="cf18a-160">Although you can select any action, for this example, we want hello Event Hubs action toosend events.</span></span>

2.  <span data-ttu-id="cf18a-161">En el cuadro de búsqueda de hello, escriba `event hubs` para el filtro.</span><span class="sxs-lookup"><span data-stu-id="cf18a-161">In hello search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="cf18a-162">Seleccione esta acción: **Enviar evento**</span><span class="sxs-lookup"><span data-stu-id="cf18a-162">Select this action: **Send event**</span></span>

    ![Seleccione la acción "Event Hubs: Enviar evento"](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="cf18a-164">Escriba los detalles de hello necesario de evento de hello, como nombre de Hola para hello concentrador de eventos donde desea que los eventos de hello toosend.</span><span class="sxs-lookup"><span data-stu-id="cf18a-164">Enter hello required details for hello event, such as hello name for hello Event Hub where you want toosend hello event.</span></span> <span data-ttu-id="cf18a-165">Escriba otros detalles acerca del evento hello, como el contenido para ese evento opcionales.</span><span class="sxs-lookup"><span data-stu-id="cf18a-165">Enter any other optional details about hello event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="cf18a-166">toooptionally especificar partición del concentrador de eventos de Hola donde toosend Hola eventos, elija **Mostrar opciones avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="cf18a-166">toooptionally specify hello Event Hub partition where toosend hello event, choose **Show advanced options**.</span></span> 

    ![Escriba el nombre del Event Hub y los detalles opcionales del evento](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="cf18a-168">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="cf18a-168">Save your changes.</span></span>

    ![Guardado de la aplicación lógica](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="cf18a-170">Ahora ha configurado un toosend de eventos de acción de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="cf18a-170">You've now set up an action toosend events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="cf18a-171">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="cf18a-171">Connector-specific details</span></span>

<span data-ttu-id="cf18a-172">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="cf18a-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="cf18a-173">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="cf18a-173">Get help</span></span>

<span data-ttu-id="cf18a-174">tooask preguntas y responder a preguntas, consulte ¿Qué otros usuarios de aplicaciones de la lógica de Azure están realizando, visitan hello [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="cf18a-174">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="cf18a-175">toohelp mejorar la lógica de aplicaciones y conectores, votar sobre o enviar ideas en hello [sitio de comentarios de usuario de las aplicaciones lógicas](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="cf18a-175">toohelp improve Logic Apps and connectors, vote on or submit ideas at hello [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf18a-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf18a-176">Next steps</span></span>

*  [<span data-ttu-id="cf18a-177">Encuentre otros conectores para Azure Logic apps</span><span class="sxs-lookup"><span data-stu-id="cf18a-177">Find other connectors for Azure Logic apps</span></span>](./apis-list.md)