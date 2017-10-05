---
title: Uso del conector de MQ en Azure Logic Apps | Microsoft Docs
description: "Conexión a un servidor local o de Azure MQ desde flujo de trabajo de la aplicación lógica para examinar, recibir y enviar mensajes a WebSphere MQ"
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 17c651585b56dae186286f5d8c68c363ae9c524d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="connect-to-an-ibm-mq-server-from-logic-apps-using-the-mq-connector"></a><span data-ttu-id="07c84-103">Conexión a un servidor IBM MQ desde las aplicaciones lógicas mediante el conector de MQ</span><span class="sxs-lookup"><span data-stu-id="07c84-103">Connect to an IBM MQ server from logic apps using the MQ connector</span></span> 

<span data-ttu-id="07c84-104">Microsoft Connector for MQ envía y recupera mensajes almacenados en un servidor MQ local o en Azure.</span><span class="sxs-lookup"><span data-stu-id="07c84-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="07c84-105">Este conector incluye un cliente de Microsoft MQ que se comunica con un servidor IBM MQ remoto a través de una red TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="07c84-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="07c84-106">Este documento es una guía de inicio para usar el conector de MQ.</span><span class="sxs-lookup"><span data-stu-id="07c84-106">This document is a starter guide to use the MQ connector.</span></span> <span data-ttu-id="07c84-107">Se recomienda empezar por explorar un mensaje de una cola y, después, intentar las demás acciones.</span><span class="sxs-lookup"><span data-stu-id="07c84-107">We recommended you begin by browsing a single message on a queue, and then trying the other actions.</span></span>    

<span data-ttu-id="07c84-108">El conector de MQ incluye las siguientes acciones.</span><span class="sxs-lookup"><span data-stu-id="07c84-108">The MQ connector includes the following actions.</span></span> <span data-ttu-id="07c84-109">No hay desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="07c84-109">There are no triggers.</span></span>

-   <span data-ttu-id="07c84-110">Examinar un único mensaje sin eliminarlo del servidor IBM MQ</span><span class="sxs-lookup"><span data-stu-id="07c84-110">Browse a single message without deleting the message from the IBM MQ Server</span></span>
-   <span data-ttu-id="07c84-111">Examinar un lote de mensajes sin eliminarlos del servidor IBM MQ</span><span class="sxs-lookup"><span data-stu-id="07c84-111">Browse a batch of messages without deleting the messages from the IBM MQ Server</span></span>
-   <span data-ttu-id="07c84-112">Recibir un único mensaje y eliminarlo del servidor IBM MQ</span><span class="sxs-lookup"><span data-stu-id="07c84-112">Receive a single message and delete the message from the IBM MQ Server</span></span>
-   <span data-ttu-id="07c84-113">Recibir un lote de mensajes y eliminarlos del servidor IBM MQ</span><span class="sxs-lookup"><span data-stu-id="07c84-113">Receive a batch of messages and delete the messages from the IBM MQ Server</span></span>
-   <span data-ttu-id="07c84-114">Enviar un único mensaje al servidor IBM MQ</span><span class="sxs-lookup"><span data-stu-id="07c84-114">Send a single message to the IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="07c84-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="07c84-115">Prerequisites</span></span>

* <span data-ttu-id="07c84-116">Si usa un servidor local de MQ, [instale la puerta de enlace de datos local](../logic-apps/logic-apps-gateway-install.md) en un servidor de la red.</span><span class="sxs-lookup"><span data-stu-id="07c84-116">If using an on-premises MQ server, [install the on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="07c84-117">Si el servidor MQ está públicamente disponible o disponible en Azure, no se necesita ni se usa la puerta de enlace de datos.</span><span class="sxs-lookup"><span data-stu-id="07c84-117">If the MQ Server is publicly available, or available within Azure, then the data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="07c84-118">El servidor donde está instalada la puerta de enlace de datos local también debe tener .Net Framework 4.6 instalado para que el conector de MQ funcione.</span><span class="sxs-lookup"><span data-stu-id="07c84-118">The server where the On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for the MQ Connector to function.</span></span>

* <span data-ttu-id="07c84-119">Cree el recurso de Azure para la puerta de enlace de datos local: [Configuración de la conexión de la puerta de enlace de datos](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="07c84-119">Create the Azure resource for the on-premises data gateway - [Set up the data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="07c84-120">Versiones oficialmente compatibles con IBM WebSphere MQ:</span><span class="sxs-lookup"><span data-stu-id="07c84-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="07c84-121">MQ 7.5</span><span class="sxs-lookup"><span data-stu-id="07c84-121">MQ 7.5</span></span>
   * <span data-ttu-id="07c84-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="07c84-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="07c84-123">Creación de una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="07c84-123">Create a logic app</span></span>

1. <span data-ttu-id="07c84-124">En el **Panel de inicio de Azure**, seleccione **+** (signo más), **Web y móvil** y después **Aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="07c84-124">In the **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="07c84-125">Rellene los campos **Nombre**, como MQTestApp, **Suscripción**, **Grupo de recursos** y **Ubicación** (use la ubicación donde esté configurada la conexión de la puerta de enlace de datos local).</span><span class="sxs-lookup"><span data-stu-id="07c84-125">Enter the **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use the location where the on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="07c84-126">Seleccione **Anclar al panel** y **Crear**.</span><span class="sxs-lookup"><span data-stu-id="07c84-126">Select **Pin to dashboard**, and select **Create**.</span></span>  
<span data-ttu-id="07c84-127">![Creación de la aplicación lógica](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="07c84-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="07c84-128">Incorporación de un desencadenador</span><span class="sxs-lookup"><span data-stu-id="07c84-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="07c84-129">El conector de MQ no tiene ningún desencadenador.</span><span class="sxs-lookup"><span data-stu-id="07c84-129">The MQ Connector does not have any triggers.</span></span> <span data-ttu-id="07c84-130">Debe usar otro desencadenador para iniciar la aplicación lógica, como **Periodicidad**.</span><span class="sxs-lookup"><span data-stu-id="07c84-130">So, use another trigger to start your logic app, such as the **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="07c84-131">Cuando se abra el **Diseñador de aplicaciones de la lógicas**, seleccione **Periodicidad** de la lista de desencadenadores comunes.</span><span class="sxs-lookup"><span data-stu-id="07c84-131">The **Logic Apps Designer** opens, select **Recurrence** in the list of common triggers.</span></span>
2. <span data-ttu-id="07c84-132">En el desencadenador Periodicidad, seleccione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="07c84-132">Select **Edit** within the Recurrence Trigger.</span></span> 
3. <span data-ttu-id="07c84-133">Establezca la **Frecuencia** en **Día**, con un **intervalo** de **7**.</span><span class="sxs-lookup"><span data-stu-id="07c84-133">Set the **Frequency** to **Day**, and set the **Interval** to **7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="07c84-134">Examen de un único mensaje</span><span class="sxs-lookup"><span data-stu-id="07c84-134">Browse a single message</span></span>
1. <span data-ttu-id="07c84-135">Seleccione **+ Nuevo paso** y **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="07c84-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="07c84-136">En el cuadro de búsqueda, escriba `mq` y seleccione **MQ - Browse message** (MQ: examinar mensaje).</span><span class="sxs-lookup"><span data-stu-id="07c84-136">In the search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="07c84-137">![Examen de un mensaje](media/connectors-create-api-mq/Browse_message.png)</span><span class="sxs-lookup"><span data-stu-id="07c84-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="07c84-138">Si no hay conexión de MQ existente, créela:</span><span class="sxs-lookup"><span data-stu-id="07c84-138">If there isn't an existing MQ connection, then create the connection:</span></span>  

    1. <span data-ttu-id="07c84-139">Seleccione **Conectarse mediante puerta de enlace de datos local** y especifique las propiedades del servidor MQ.</span><span class="sxs-lookup"><span data-stu-id="07c84-139">Select **Connect via on-premises data gateway**, and enter the properties of your MQ server.</span></span>  
    <span data-ttu-id="07c84-140">Para **Servidor**, especifique el nombre del servidor MQ, o escriba la dirección IP seguida de dos puntos y el número del puerto.</span><span class="sxs-lookup"><span data-stu-id="07c84-140">For **Server**, you can enter the MQ server name, or enter the IP address followed by a colon and the port number.</span></span> 
    2. <span data-ttu-id="07c84-141">La lista desplegable de **puertas de enlace** muestra las conexiones de puerta de enlace existentes configuradas.</span><span class="sxs-lookup"><span data-stu-id="07c84-141">The **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="07c84-142">Seleccione la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="07c84-142">Select your gateway.</span></span>
    3. <span data-ttu-id="07c84-143">Cuando haya terminado, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="07c84-143">Select **Create** when finished.</span></span> <span data-ttu-id="07c84-144">La conexión se parecerá a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="07c84-144">Your connection looks similar to the following:</span></span>   
    <span data-ttu-id="07c84-145">![Propiedades de la conexión](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="07c84-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="07c84-146">En las propiedades de acción, puede:</span><span class="sxs-lookup"><span data-stu-id="07c84-146">In the action properties, you can:</span></span>  

    * <span data-ttu-id="07c84-147">Use la propiedad **Queue** para acceder a un nombre de cola distinto al que se define en la conexión</span><span class="sxs-lookup"><span data-stu-id="07c84-147">Use the **Queue** property to access a different queue name than what is defined in the connection</span></span>
    * <span data-ttu-id="07c84-148">Usar las propiedades **MessageId**, **CorrelationId**, **GroupId** y otras para buscar un mensaje en función de las distintas propiedades de los mensajes de MQ</span><span class="sxs-lookup"><span data-stu-id="07c84-148">Use the **MessageId**, **CorrelationId**, **GroupId**, and other properties to browse for a message based on the different MQ message properties</span></span>
    * <span data-ttu-id="07c84-149">Establecer **IncludeInfo** en **True** para incluir información adicional al mensaje de salida.</span><span class="sxs-lookup"><span data-stu-id="07c84-149">Set **IncludeInfo** to **True** to include additional message information in the output.</span></span> <span data-ttu-id="07c84-150">O establecerlo en **False** para no incluir información adicional al mensaje de salida.</span><span class="sxs-lookup"><span data-stu-id="07c84-150">Or, set it to **False** to not include additional message information in the output.</span></span>
    * <span data-ttu-id="07c84-151">Escribir un valor para **Timeout** para determinar cuánto tiempo esperar a que llegue un mensaje a una cola vacía.</span><span class="sxs-lookup"><span data-stu-id="07c84-151">Enter a **Timeout** value to determine how long to wait for a message to arrive in an empty queue.</span></span> <span data-ttu-id="07c84-152">Si no se especifica nada, se recupera el primer mensaje de la cola y no hay tiempo de espera para que aparezca un mensaje.</span><span class="sxs-lookup"><span data-stu-id="07c84-152">If nothing is entered, the first message in the queue is retrieved, and there is no time spent waiting for a message to appear.</span></span>  
    <span data-ttu-id="07c84-153">![Propiedades de Browse message](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="07c84-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="07c84-154">Haga clic en **Guardar** para guardar los cambios y en **Ejecutar** para ejecutar la aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="07c84-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="07c84-155">![Guardar y ejecutar](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="07c84-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="07c84-156">Después de unos segundos, los pasos de la ejecución aparecerán y podrá observar la salida.</span><span class="sxs-lookup"><span data-stu-id="07c84-156">After a few seconds, the steps of the run are shown, and you can look at the output.</span></span> <span data-ttu-id="07c84-157">Seleccione la marca de verificación verde para ver los detalles de cada paso.</span><span class="sxs-lookup"><span data-stu-id="07c84-157">Select the green checkmark to see details of each step.</span></span> <span data-ttu-id="07c84-158">Seleccione **Mostrar salidas sin procesar** para ver más detalles de los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="07c84-158">Select **See raw outputs** to see additional details on the output data.</span></span>  
<span data-ttu-id="07c84-159">![Salida de Browse message](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="07c84-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="07c84-160">Salida sin procesar:</span><span class="sxs-lookup"><span data-stu-id="07c84-160">Raw output:</span></span>  
    ![Salida sin procesar de Browse message](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="07c84-162">Cuando la opción **IncludeInfo** se establece en true, aparece el resultado siguiente:</span><span class="sxs-lookup"><span data-stu-id="07c84-162">When the **IncludeInfo** option is set to true, the following output is displayed:</span></span>  
<span data-ttu-id="07c84-163">![IncludeInfo de Browse message](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="07c84-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="07c84-164">Examen de varios mensajes</span><span class="sxs-lookup"><span data-stu-id="07c84-164">Browse multiple messages</span></span>
<span data-ttu-id="07c84-165">La acción **Browse messages** incluye la opción **BatchSize** para indicar cuántos mensajes se deben devolver de la cola.</span><span class="sxs-lookup"><span data-stu-id="07c84-165">The **Browse messages** action includes a **BatchSize** option to indicate how many messages should be returned from the queue.</span></span>  <span data-ttu-id="07c84-166">Si **BatchSize** se deja en blanco, se devuelven todos los mensajes.</span><span class="sxs-lookup"><span data-stu-id="07c84-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="07c84-167">El resultado devuelto es una matriz de mensajes.</span><span class="sxs-lookup"><span data-stu-id="07c84-167">The returned output is an array of messages.</span></span>

1. <span data-ttu-id="07c84-168">Al agregar la acción **Browse messages**, la primera conexión configurada se selecciona de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="07c84-168">When adding the **Browse messages** action, the first connection that is configured is selected by default.</span></span> <span data-ttu-id="07c84-169">Seleccione **Cambiar conexión** para crear una conexión nueva o seleccione una diferente.</span><span class="sxs-lookup"><span data-stu-id="07c84-169">Select **Change connection** to create a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="07c84-170">La salida de Browse messages muestra:</span><span class="sxs-lookup"><span data-stu-id="07c84-170">The output of Browse messages shows:</span></span>  
![Salida de Browse message](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="07c84-172">Recepción de un único mensaje</span><span class="sxs-lookup"><span data-stu-id="07c84-172">Receive a single message</span></span>
<span data-ttu-id="07c84-173">La acción **Receive message** tiene las mismas entradas y salidas que la acción **Browse message**.</span><span class="sxs-lookup"><span data-stu-id="07c84-173">The **Receive message** action has the same inputs and outputs as the **Browse message** action.</span></span> <span data-ttu-id="07c84-174">Cuando se usa **Receive message**, el mensaje se elimina de la cola.</span><span class="sxs-lookup"><span data-stu-id="07c84-174">When using **Receive message**, the message is deleted from the queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="07c84-175">Recepción de varios mensajes</span><span class="sxs-lookup"><span data-stu-id="07c84-175">Receive multiple messages</span></span>
<span data-ttu-id="07c84-176">La acción **Receive messages** tiene las mismas entradas y salidas que la acción **Browse messages**.</span><span class="sxs-lookup"><span data-stu-id="07c84-176">The **Receive messages** action has the same inputs and outputs as the **Browse messages** action.</span></span> <span data-ttu-id="07c84-177">Cuando se usa **Receive messages**, los mensajes se eliminan de la cola.</span><span class="sxs-lookup"><span data-stu-id="07c84-177">When using **Receive messages**, the messages are deleted from the queue.</span></span>

<span data-ttu-id="07c84-178">Si no hay mensajes en la cola al realizar la acción browse o receive, el paso produce un error con la siguiente salida:</span><span class="sxs-lookup"><span data-stu-id="07c84-178">If there are no messages in the queue when doing a browse or a receive, the step fails with the following output:</span></span>  
![Error de ausencia de mensajes en MQ](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="07c84-180">Envío de un mensaje</span><span class="sxs-lookup"><span data-stu-id="07c84-180">Send a message</span></span>
1. <span data-ttu-id="07c84-181">Al agregar la acción **Send message**, la primera conexión configurada se selecciona de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="07c84-181">When adding the **Send message** action, the first connection that is configured is selected by default.</span></span> <span data-ttu-id="07c84-182">Seleccione **Cambiar conexión** para crear una conexión nueva o seleccione una diferente.</span><span class="sxs-lookup"><span data-stu-id="07c84-182">Select **Change connection** to create a new connection, or select a different connection.</span></span> <span data-ttu-id="07c84-183">Los valores válidos para **Message Types** son **Datagram**, **Reply** o **Request**.</span><span class="sxs-lookup"><span data-stu-id="07c84-183">The valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="07c84-184">![Propiedades de Send message](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="07c84-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="07c84-185">La salida de Send message tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="07c84-185">The output of Send message looks like the following:</span></span>  
![Salida de Send message](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="07c84-187">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="07c84-187">Connector-specific details</span></span>

<span data-ttu-id="07c84-188">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/mq/).</span><span class="sxs-lookup"><span data-stu-id="07c84-188">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="07c84-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="07c84-189">Next steps</span></span>
<span data-ttu-id="07c84-190">[Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="07c84-190">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="07c84-191">Explore los demás conectores disponibles en Logic Apps en nuestra [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="07c84-191">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
