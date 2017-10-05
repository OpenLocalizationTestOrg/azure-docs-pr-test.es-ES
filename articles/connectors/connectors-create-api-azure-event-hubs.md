---
title: "Configurar la supervisión de eventos con Azure Event Hubs para Azure Logic Apps | Microsoft Docs"
description: Supervisar flujos de datos para recibir eventos y enviar eventos para Azure Logic Apps con Azure Event Hubs
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
ms.openlocfilehash: 2ca27fb8269d1796fb1181fc4d0a8744a592d548
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-receive-and-send-events-with-the-event-hubs-connector"></a><span data-ttu-id="3d26a-104">Supervisar, recibir y enviar eventos con el conector de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3d26a-104">Monitor, receive, and send events with the Event Hubs connector</span></span>

<span data-ttu-id="3d26a-105">Para configurar la supervisión de eventos para que su aplicación lógica pueda detectar eventos, recibir eventos y enviar eventos, conéctese a un [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs) desde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="3d26a-105">To set up an event monitor so that your logic app can detect events, receive events, and send events, connect to an [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="3d26a-106">Obtenga más información acerca de los [Centros de eventos de Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="3d26a-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="3d26a-107">Requisitos</span><span class="sxs-lookup"><span data-stu-id="3d26a-107">Requirements</span></span>

* <span data-ttu-id="3d26a-108">Debe tener un [espacio de nombres de Event Hubs y un Event Hub](../event-hubs/event-hubs-create.md) en Azure.</span><span class="sxs-lookup"><span data-stu-id="3d26a-108">You have to have an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="3d26a-109">Obtenga información sobre [cómo crear un espacio de nombres de Event Hubs y un Event Hub](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="3d26a-109">Learn [how to create an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="3d26a-110">Para usar [cualquier conector](https://docs.microsoft.com/azure/connectors/apis-list) en su aplicación lógica, primero debe crearla.</span><span class="sxs-lookup"><span data-stu-id="3d26a-110">To use [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have to create a logic app first.</span></span> <span data-ttu-id="3d26a-111">Obtenga información sobre [cómo crear una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3d26a-111">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-the-connection-string"></a><span data-ttu-id="3d26a-112">Comprobar los permisos del espacio de nombres de Event Hubs y buscar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="3d26a-112">Check Event Hubs namespace permissions and find the connection string</span></span>

<span data-ttu-id="3d26a-113">Para que la aplicación lógica tenga acceso a cualquier servicio, tendrá que crear una [*conexión*](./connectors-overview.md) entre la aplicación lógica y el servicio, si todavía no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="3d26a-113">For your logic app to access any service, you have to create a [*connection*](./connectors-overview.md) between your logic app and the service, if you haven't already.</span></span> <span data-ttu-id="3d26a-114">Esta conexión autoriza a la aplicación lógica a acceder a los datos.</span><span class="sxs-lookup"><span data-stu-id="3d26a-114">This connection authorizes your logic app to access data.</span></span>
<span data-ttu-id="3d26a-115">Para que la aplicación lógica acceda a su Event Hub, debe tener permisos de **Administrador** y la cadena de conexión para el espacio de nombres del Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="3d26a-115">For your logic app to access your Event Hub, you have to have **Manage** permissions and the connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="3d26a-116">Para comprobar sus permisos y obtener la cadena de conexión, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="3d26a-116">To check your permissions and get the connection string, follow these steps.</span></span>

1.  <span data-ttu-id="3d26a-117">Inicie sesión en [Azure Portal](https://portal.azure.com "Azure Portal").</span><span class="sxs-lookup"><span data-stu-id="3d26a-117">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="3d26a-118">Vaya al *espacio de nombres* de los Event Hubs, no al Event Hub específico.</span><span class="sxs-lookup"><span data-stu-id="3d26a-118">Go to your Event Hubs *namespace*, not the specific Event Hub.</span></span> <span data-ttu-id="3d26a-119">En la hoja del espacio de nombres, haga clic en **Configuración** y elija **Políticas de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="3d26a-119">On the namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="3d26a-120">En **Notificaciones**, compruebe que tenga permisos de **Administrador** para ese espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="3d26a-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![Administrar los permisos del espacio de nombres del Event Hub](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="3d26a-122">Para copiar la cadena de conexión para el espacio de nombres de Event Hubs, elija **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="3d26a-122">To copy the connection string for the Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="3d26a-123">Al lado de la cadena de conexión de su clave principal, elija el botón Copiar.</span><span class="sxs-lookup"><span data-stu-id="3d26a-123">Next to your primary key connection string, choose the copy button.</span></span>

    ![Copie la cadena de conexión del espacio de nombres de los Event Hubs](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="3d26a-125">Para confirmar si la cadena de conexión está asociada con el espacio de nombres de los Event Hubs o con un Event Hub específico, compruebe la cadena de conexión para el parámetro `EntityPath`.</span><span class="sxs-lookup"><span data-stu-id="3d26a-125">To confirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check the connection string for the `EntityPath` parameter.</span></span> <span data-ttu-id="3d26a-126">Si encuentra este parámetro, la cadena de conexión es para la "entidad" de un Event Hub específico y no es la cadena correcta para utilizar con la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="3d26a-126">If you find this parameter, the connection string is for a specific Event Hub "entity", and is not the correct string to use with your logic app.</span></span>

4.  <span data-ttu-id="3d26a-127">Cuando se le soliciten las credenciales después de agregar un desencadenador de los Event Hubs o la acción a la aplicación lógica, puede conectarse al espacio de nombres de los Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="3d26a-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action to your logic app, you can connect to your Event Hubs namespace.</span></span> <span data-ttu-id="3d26a-128">Asigne un nombre a la conexión, ingrese la cadena de conexión que copió y elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3d26a-128">Give your connection a name, enter the connection string that you copied, and choose **Create**.</span></span>

    ![Ingrese la cadena de conexión para el espacio de nombres de los Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="3d26a-130">Después de crear la conexión, su nombre debe aparecer en el desencadenador o la acción de los Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="3d26a-130">After you create your connection, the connection name should appear in the Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="3d26a-131">Ahora puede continuar con el resto de los pasos en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="3d26a-131">You can then continue with the other steps in your logic app.</span></span>

    ![Conexión del espacio de nombres de los Event Hubs creada](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="3d26a-133">Iniciar el flujo de trabajo cuando el Event Hub recibe eventos nuevos</span><span class="sxs-lookup"><span data-stu-id="3d26a-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="3d26a-134">Un [*desencadenador*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) es un evento que inicia un flujo de trabajo en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="3d26a-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="3d26a-135">Para iniciar un flujo de trabajo cuando se envían nuevos eventos al Event Hub, siga estos pasos para agregar el desencadenador que detecta este evento.</span><span class="sxs-lookup"><span data-stu-id="3d26a-135">To start a workflow when new events are sent to your Event Hub, follow these steps for adding the trigger that detects this event.</span></span>

1.  <span data-ttu-id="3d26a-136">En [Azure Portal](https://portal.azure.com "Azure Portal"), vaya a la aplicación lógica existente o cree una aplicación de lógica en blanco.</span><span class="sxs-lookup"><span data-stu-id="3d26a-136">In the [Azure portal](https://portal.azure.com "Azure portal"), go to your existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="3d26a-137">En el cuadro de búsqueda del diseñador de aplicaciones lógicas, ingrese `event hubs` para el filtro.</span><span class="sxs-lookup"><span data-stu-id="3d26a-137">In the search box for the Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="3d26a-138">Seleccione este desencadenador: **Cuando los eventos estén disponibles en el Event Hub**</span><span class="sxs-lookup"><span data-stu-id="3d26a-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![Seleccione el desencadenador para cuando el Event Hub reciba eventos nuevos](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="3d26a-140">Si todavía no tiene una conexión al espacio de nombres de los Event Hubs, se le pedirá que cree ahora esta conexión.</span><span class="sxs-lookup"><span data-stu-id="3d26a-140">If you don't already have a connection to your Event Hubs namespace, you're prompted to create this connection now.</span></span> <span data-ttu-id="3d26a-141">Asigne un nombre a la conexión e ingrese la cadena de conexión para el espacio de nombres de los Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="3d26a-141">Give your connection a name, and enter the connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="3d26a-142">Si es necesario, obtenga información acerca de [cómo buscar la cadena de conexión](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="3d26a-142">If necessary, learn [how to find your connection string](#permissions-connection-string).</span></span>

    ![Ingrese la cadena de conexión para el espacio de nombres de los Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="3d26a-144">Después de crear la conexión, aparecerá la configuración del desencadenador **Cuando los eventos estén disponibles en el Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="3d26a-144">After you create the connection, the settings for the **When an event in available in an Event Hub** trigger appear.</span></span>

    ![Configuración del desencadenador para cuando el Event Hub reciba eventos nuevos](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="3d26a-146">Escriba o seleccione el nombre para el Event Hub que desea supervisar.</span><span class="sxs-lookup"><span data-stu-id="3d26a-146">Enter or select the name for the Event Hub that you want to monitor.</span></span> <span data-ttu-id="3d26a-147">Seleccione la frecuencia y el intervalo con el que desea revisar el Event Hub.</span><span class="sxs-lookup"><span data-stu-id="3d26a-147">Select the frequency and interval for how often you want to check the Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="3d26a-148">Si desea, opcionalmente, seleccionar un grupo de consumidores para leer los eventos, elija **Mostrar opciones avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="3d26a-148">To optionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![Especificar Event Hub o grupo de consumidores](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="3d26a-150">Ya ha configurado un desencadenador para iniciar un flujo de trabajo para la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="3d26a-150">You've now set up a trigger to start a workflow for your logic app.</span></span> 
    <span data-ttu-id="3d26a-151">La aplicación lógica comprueba el Event Hub especificado según la programación que haya establecido.</span><span class="sxs-lookup"><span data-stu-id="3d26a-151">Your logic app checks the specified Event Hub based on the schedule that you set.</span></span> 
    <span data-ttu-id="3d26a-152">Si la aplicación detecta nuevos eventos en el Event Hub, el desencadenador ejecutará otras acciones o desencadenadores en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="3d26a-152">If your app finds new events in the Event Hub, the trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-to-your-event-hub-from-your-logic-app"></a><span data-ttu-id="3d26a-153">Enviar eventos al Event Hub desde la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="3d26a-153">Send events to your Event Hub from your logic app</span></span>

<span data-ttu-id="3d26a-154">Una [*acción*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) es una tarea realizada por el flujo de trabajo de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="3d26a-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="3d26a-155">Después de agregar un desencadenador a la aplicación lógica, puede agregar una acción para llevar a cabo operaciones con los datos generados por ese desencadenador.</span><span class="sxs-lookup"><span data-stu-id="3d26a-155">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="3d26a-156">Para enviar eventos al Event Hub desde la aplicación lógica, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="3d26a-156">To send an event to your Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="3d26a-157">En el Diseñador de aplicaciones lógicas, bajo el desencadenador de la aplicación lógica, elija **Nuevo paso** > **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="3d26a-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    ![Haga clic en "Nuevo paso" y en "Agregar una acción"](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="3d26a-159">Ahora puede buscar y seleccionar la acción que desea realizar.</span><span class="sxs-lookup"><span data-stu-id="3d26a-159">Now you can find and select an action to perform.</span></span> 
    <span data-ttu-id="3d26a-160">Aunque puede seleccionar cualquier acción, en este ejemplo, queremos que la acción de los Event Hubs envíe eventos.</span><span class="sxs-lookup"><span data-stu-id="3d26a-160">Although you can select any action, for this example, we want the Event Hubs action to send events.</span></span>

2.  <span data-ttu-id="3d26a-161">En el cuadro de búsqueda, escriba`event hubs` para el filtro.</span><span class="sxs-lookup"><span data-stu-id="3d26a-161">In the search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="3d26a-162">Seleccione esta acción: **Enviar evento**</span><span class="sxs-lookup"><span data-stu-id="3d26a-162">Select this action: **Send event**</span></span>

    ![Seleccione la acción "Event Hubs: Enviar evento"](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="3d26a-164">Ingrese los detalles necesarios para el evento, como el nombre para el Event Hub al que desea enviar el evento.</span><span class="sxs-lookup"><span data-stu-id="3d26a-164">Enter the required details for the event, such as the name for the Event Hub where you want to send the event.</span></span> <span data-ttu-id="3d26a-165">Escriba cualquier otro detalle sobre el evento, como el contenido para ese evento.</span><span class="sxs-lookup"><span data-stu-id="3d26a-165">Enter any other optional details about the event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="3d26a-166">Para especificar la partición del Event Hub a la cual enviar el evento, elija **Mostrar opciones avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="3d26a-166">To optionally specify the Event Hub partition where to send the event, choose **Show advanced options**.</span></span> 

    ![Escriba el nombre del Event Hub y los detalles opcionales del evento](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="3d26a-168">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="3d26a-168">Save your changes.</span></span>

    ![Guardado de la aplicación lógica](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="3d26a-170">Ahora ha configurado una acción para enviar eventos desde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="3d26a-170">You've now set up an action to send events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="3d26a-171">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="3d26a-171">Connector-specific details</span></span>

<span data-ttu-id="3d26a-172">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="3d26a-172">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="3d26a-173">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="3d26a-173">Get help</span></span>

<span data-ttu-id="3d26a-174">Para formular preguntas, o responderlas, y ver lo que hacen otros usuarios de Azure Logic Apps, visite el [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="3d26a-174">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="3d26a-175">Para ayudar a mejorar Logic Apps y los conectores, vote o envíe ideas en el [sitio de comentarios de usuario de Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="3d26a-175">To help improve Logic Apps and connectors, vote on or submit ideas at the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d26a-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3d26a-176">Next steps</span></span>

*  [<span data-ttu-id="3d26a-177">Encuentre otros conectores para Azure Logic apps</span><span class="sxs-lookup"><span data-stu-id="3d26a-177">Find other connectors for Azure Logic apps</span></span>](./apis-list.md)