---
title: "aaaLearn cómo toouse Hola conector MQ en las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Conecte tooan local o servidor MQ de Azure de su toobrowse de flujo de trabajo de aplicación lógica, recibir y enviar mensajes tooWebSphere MQ"
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
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a><span data-ttu-id="71bcb-103">Conectar tooan servidor MQ de IBM desde las aplicaciones lógicas mediante el conector MQ Hola</span><span class="sxs-lookup"><span data-stu-id="71bcb-103">Connect tooan IBM MQ server from logic apps using hello MQ connector</span></span> 

<span data-ttu-id="71bcb-104">Microsoft Connector for MQ envía y recupera mensajes almacenados en un servidor MQ local o en Azure.</span><span class="sxs-lookup"><span data-stu-id="71bcb-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="71bcb-105">Este conector incluye un cliente de Microsoft MQ que se comunica con un servidor IBM MQ remoto a través de una red TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="71bcb-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="71bcb-106">Este documento es un conector MQ starter guía toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="71bcb-106">This document is a starter guide toouse hello MQ connector.</span></span> <span data-ttu-id="71bcb-107">Se recomienda empezar examinando un único mensaje en una cola y, a continuación, intentar Hola otras acciones.</span><span class="sxs-lookup"><span data-stu-id="71bcb-107">We recommended you begin by browsing a single message on a queue, and then trying hello other actions.</span></span>    

<span data-ttu-id="71bcb-108">conector MQ Hola incluye Hola siguientes acciones.</span><span class="sxs-lookup"><span data-stu-id="71bcb-108">hello MQ connector includes hello following actions.</span></span> <span data-ttu-id="71bcb-109">No hay desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="71bcb-109">There are no triggers.</span></span>

-   <span data-ttu-id="71bcb-110">Examinar un único mensaje sin eliminar los mensajes de bienvenida de hello servidor MQ de IBM</span><span class="sxs-lookup"><span data-stu-id="71bcb-110">Browse a single message without deleting hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="71bcb-111">Examinar un lote de mensajes sin eliminar los mensajes de saludo de hello servidor MQ de IBM</span><span class="sxs-lookup"><span data-stu-id="71bcb-111">Browse a batch of messages without deleting hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="71bcb-112">Recibir un mensaje único y eliminar mensajes de bienvenida de Hola servidor MQ de IBM</span><span class="sxs-lookup"><span data-stu-id="71bcb-112">Receive a single message and delete hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="71bcb-113">Recibir un lote de mensajes y eliminar mensajes de saludo de hello servidor MQ de IBM</span><span class="sxs-lookup"><span data-stu-id="71bcb-113">Receive a batch of messages and delete hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="71bcb-114">Enviar un toohello de mensaje único servidor MQ de IBM</span><span class="sxs-lookup"><span data-stu-id="71bcb-114">Send a single message toohello IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="71bcb-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="71bcb-115">Prerequisites</span></span>

* <span data-ttu-id="71bcb-116">Si usa un servidor local de MQ, [instalar la puerta de enlace de datos de hello local](../logic-apps/logic-apps-gateway-install.md) en un servidor dentro de la red.</span><span class="sxs-lookup"><span data-stu-id="71bcb-116">If using an on-premises MQ server, [install hello on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="71bcb-117">Si Hola MQ Server está públicamente disponible o está disponible dentro de Azure, puerta de enlace de datos de hello no se utilicen o requerido.</span><span class="sxs-lookup"><span data-stu-id="71bcb-117">If hello MQ Server is publicly available, or available within Azure, then hello data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="71bcb-118">servidor de Hola donde hello puerta de enlace de datos local se instala también debe tener .net Framework 4.6 instalado para hello MQ conector toofunction.</span><span class="sxs-lookup"><span data-stu-id="71bcb-118">hello server where hello On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for hello MQ Connector toofunction.</span></span>

* <span data-ttu-id="71bcb-119">Crear recursos de Azure para puerta de enlace de datos de local de hello - hello [configurar conexión de puerta de enlace de datos de hello](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="71bcb-119">Create hello Azure resource for hello on-premises data gateway - [Set up hello data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="71bcb-120">Versiones oficialmente compatibles con IBM WebSphere MQ:</span><span class="sxs-lookup"><span data-stu-id="71bcb-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="71bcb-121">MQ 7.5</span><span class="sxs-lookup"><span data-stu-id="71bcb-121">MQ 7.5</span></span>
   * <span data-ttu-id="71bcb-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="71bcb-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="71bcb-123">Creación de una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="71bcb-123">Create a logic app</span></span>

1. <span data-ttu-id="71bcb-124">Hola **Azure iniciar panel**, seleccione  **+**  (signo más), **Web y móvil**y, a continuación, **aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="71bcb-124">In hello **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="71bcb-125">Escriba hello **nombre**, como MQTestApp, **suscripción**, **grupo de recursos**, y **ubicación** (usar ubicación Hola donde hello conexión de puerta de enlace de datos local está configurado).</span><span class="sxs-lookup"><span data-stu-id="71bcb-125">Enter hello **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use hello location where hello on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="71bcb-126">Seleccione **Pin toodashboard**y seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="71bcb-126">Select **Pin toodashboard**, and select **Create**.</span></span>  
<span data-ttu-id="71bcb-127">![Creación de la aplicación lógica](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="71bcb-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="71bcb-128">Incorporación de un desencadenador</span><span class="sxs-lookup"><span data-stu-id="71bcb-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="71bcb-129">Hola MQ conector no tiene los desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="71bcb-129">hello MQ Connector does not have any triggers.</span></span> <span data-ttu-id="71bcb-130">Por lo tanto, use otro toostart desencadenador la aplicación lógica, como hello **periodicidad** desencadenador.</span><span class="sxs-lookup"><span data-stu-id="71bcb-130">So, use another trigger toostart your logic app, such as hello **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="71bcb-131">Hola **el Diseñador de aplicaciones de la lógica de** se abre, seleccione **periodicidad** en lista de hello del modo habitual.</span><span class="sxs-lookup"><span data-stu-id="71bcb-131">hello **Logic Apps Designer** opens, select **Recurrence** in hello list of common triggers.</span></span>
2. <span data-ttu-id="71bcb-132">Seleccione **editar** dentro de hello desencadenador de periodicidad.</span><span class="sxs-lookup"><span data-stu-id="71bcb-132">Select **Edit** within hello Recurrence Trigger.</span></span> 
3. <span data-ttu-id="71bcb-133">Conjunto hello **frecuencia** demasiado**día**, conjunto hello y **intervalo** demasiado**7**.</span><span class="sxs-lookup"><span data-stu-id="71bcb-133">Set hello **Frequency** too**Day**, and set hello **Interval** too**7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="71bcb-134">Examen de un único mensaje</span><span class="sxs-lookup"><span data-stu-id="71bcb-134">Browse a single message</span></span>
1. <span data-ttu-id="71bcb-135">Seleccione **+ Nuevo paso** y **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="71bcb-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="71bcb-136">En el cuadro de búsqueda de hello, escriba `mq`y, a continuación, seleccione **MQ - examinar mensajes**.</span><span class="sxs-lookup"><span data-stu-id="71bcb-136">In hello search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="71bcb-137">![Examen de un mensaje](media/connectors-create-api-mq/Browse_message.png)</span><span class="sxs-lookup"><span data-stu-id="71bcb-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="71bcb-138">Si no hay una conexión de MQ existente, a continuación, crear la conexión de hello:</span><span class="sxs-lookup"><span data-stu-id="71bcb-138">If there isn't an existing MQ connection, then create hello connection:</span></span>  

    1. <span data-ttu-id="71bcb-139">Seleccione **conectar a través de puerta de enlace de datos local**y especifique las propiedades de saludo del servidor MQ.</span><span class="sxs-lookup"><span data-stu-id="71bcb-139">Select **Connect via on-premises data gateway**, and enter hello properties of your MQ server.</span></span>  
    <span data-ttu-id="71bcb-140">Para **Server**, puede especificar nombre del servidor MQ hello, o escriba dirección IP de hello seguido por un número de puerto hello y dos puntos.</span><span class="sxs-lookup"><span data-stu-id="71bcb-140">For **Server**, you can enter hello MQ server name, or enter hello IP address followed by a colon and hello port number.</span></span> 
    2. <span data-ttu-id="71bcb-141">Hola **puerta de enlace** lista desplegable muestra las conexiones de puerta de enlace existentes que se han configurado.</span><span class="sxs-lookup"><span data-stu-id="71bcb-141">hello **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="71bcb-142">Seleccione la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="71bcb-142">Select your gateway.</span></span>
    3. <span data-ttu-id="71bcb-143">Cuando haya terminado, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="71bcb-143">Select **Create** when finished.</span></span> <span data-ttu-id="71bcb-144">La conexión tiene un aspecto similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="71bcb-144">Your connection looks similar toohello following:</span></span>   
    <span data-ttu-id="71bcb-145">![Propiedades de la conexión](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="71bcb-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="71bcb-146">En Propiedades de la acción de hello, puede:</span><span class="sxs-lookup"><span data-stu-id="71bcb-146">In hello action properties, you can:</span></span>  

    * <span data-ttu-id="71bcb-147">Hola de uso **cola** propiedad tooaccess otro nombre de cola a la que se define en la conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="71bcb-147">Use hello **Queue** property tooaccess a different queue name than what is defined in hello connection</span></span>
    * <span data-ttu-id="71bcb-148">Hola de uso **MessageId**, **CorrelationId**, **GroupId**y otro toobrowse de propiedades para un mensaje basándose en Propiedades de mensaje de Hola diferentes MQ</span><span class="sxs-lookup"><span data-stu-id="71bcb-148">Use hello **MessageId**, **CorrelationId**, **GroupId**, and other properties toobrowse for a message based on hello different MQ message properties</span></span>
    * <span data-ttu-id="71bcb-149">Establecer **IncludeInfo** demasiado**True** tooinclude información de mensaje adicional en la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="71bcb-149">Set **IncludeInfo** too**True** tooinclude additional message information in hello output.</span></span> <span data-ttu-id="71bcb-150">O bien, establezca esta opción demasiado**False** toonot incluir información de los mensajes adicionales en el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="71bcb-150">Or, set it too**False** toonot include additional message information in hello output.</span></span>
    * <span data-ttu-id="71bcb-151">Escriba un **tiempo de espera** toodetermine valor cuánto toowait para un tooarrive de mensaje en una cola vacía.</span><span class="sxs-lookup"><span data-stu-id="71bcb-151">Enter a **Timeout** value toodetermine how long toowait for a message tooarrive in an empty queue.</span></span> <span data-ttu-id="71bcb-152">Si no se especifica nada, se recupera el primer mensaje de Hola de cola de hello y no hay ningún tiempo de espera empleado para un mensaje tooappear.</span><span class="sxs-lookup"><span data-stu-id="71bcb-152">If nothing is entered, hello first message in hello queue is retrieved, and there is no time spent waiting for a message tooappear.</span></span>  
    <span data-ttu-id="71bcb-153">![Propiedades de Browse message](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="71bcb-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="71bcb-154">Haga clic en **Guardar** para guardar los cambios y en **Ejecutar** para ejecutar la aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="71bcb-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="71bcb-155">![Guardar y ejecutar](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="71bcb-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="71bcb-156">Después de unos segundos, se muestran los pasos de Hola de hello ejecutar y puede mirar la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="71bcb-156">After a few seconds, hello steps of hello run are shown, and you can look at hello output.</span></span> <span data-ttu-id="71bcb-157">Seleccione Hola marca de verificación verde toosee detalles de cada paso.</span><span class="sxs-lookup"><span data-stu-id="71bcb-157">Select hello green checkmark toosee details of each step.</span></span> <span data-ttu-id="71bcb-158">Seleccione **ver resultados sin formato** toosee detalles adicionales en hello los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="71bcb-158">Select **See raw outputs** toosee additional details on hello output data.</span></span>  
<span data-ttu-id="71bcb-159">![Salida de Browse message](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="71bcb-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="71bcb-160">Salida sin procesar:</span><span class="sxs-lookup"><span data-stu-id="71bcb-160">Raw output:</span></span>  
    ![Salida sin procesar de Browse message](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="71bcb-162">Cuando Hola **IncludeInfo** opción se establece tootrue, se muestra hello después de salida:</span><span class="sxs-lookup"><span data-stu-id="71bcb-162">When hello **IncludeInfo** option is set tootrue, hello following output is displayed:</span></span>  
<span data-ttu-id="71bcb-163">![IncludeInfo de Browse message](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="71bcb-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="71bcb-164">Examen de varios mensajes</span><span class="sxs-lookup"><span data-stu-id="71bcb-164">Browse multiple messages</span></span>
<span data-ttu-id="71bcb-165">Hola **examinar mensajes** acción incluye una **BatchSize** opción tooindicate cuántos mensajes se deben devolver desde la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="71bcb-165">hello **Browse messages** action includes a **BatchSize** option tooindicate how many messages should be returned from hello queue.</span></span>  <span data-ttu-id="71bcb-166">Si **BatchSize** se deja en blanco, se devuelven todos los mensajes.</span><span class="sxs-lookup"><span data-stu-id="71bcb-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="71bcb-167">Hola devuelve el resultado es una matriz de mensajes.</span><span class="sxs-lookup"><span data-stu-id="71bcb-167">hello returned output is an array of messages.</span></span>

1. <span data-ttu-id="71bcb-168">Al agregar hello **examinar mensajes** acción, conexión primera Hola que está configurado de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="71bcb-168">When adding hello **Browse messages** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="71bcb-169">Seleccione **cambiar conexión** toocreate una conexión nueva, o seleccione otra conexión.</span><span class="sxs-lookup"><span data-stu-id="71bcb-169">Select **Change connection** toocreate a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="71bcb-170">salida de Hello de examinar mensajes de muestra:</span><span class="sxs-lookup"><span data-stu-id="71bcb-170">hello output of Browse messages shows:</span></span>  
![Salida de Browse message](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="71bcb-172">Recepción de un único mensaje</span><span class="sxs-lookup"><span data-stu-id="71bcb-172">Receive a single message</span></span>
<span data-ttu-id="71bcb-173">Hola **recibir mensaje** acción ha Hola mismo entradas y salidas como hello **examinar mensajes** acción.</span><span class="sxs-lookup"><span data-stu-id="71bcb-173">hello **Receive message** action has hello same inputs and outputs as hello **Browse message** action.</span></span> <span data-ttu-id="71bcb-174">Cuando se usa **recibir mensaje**, mensaje de bienvenida se elimina de la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="71bcb-174">When using **Receive message**, hello message is deleted from hello queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="71bcb-175">Recepción de varios mensajes</span><span class="sxs-lookup"><span data-stu-id="71bcb-175">Receive multiple messages</span></span>
<span data-ttu-id="71bcb-176">Hola **recibir mensajes** acción ha Hola mismo entradas y salidas como hello **examinar mensajes** acción.</span><span class="sxs-lookup"><span data-stu-id="71bcb-176">hello **Receive messages** action has hello same inputs and outputs as hello **Browse messages** action.</span></span> <span data-ttu-id="71bcb-177">Cuando se usa **recibir mensajes**, se eliminan mensajes de saludo de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="71bcb-177">When using **Receive messages**, hello messages are deleted from hello queue.</span></span>

<span data-ttu-id="71bcb-178">Si no hay ningún mensaje en cola Hola al realizar un examen o una operación de recepción, se produce un error en la paso Hola con hello después de salida:</span><span class="sxs-lookup"><span data-stu-id="71bcb-178">If there are no messages in hello queue when doing a browse or a receive, hello step fails with hello following output:</span></span>  
![Error de ausencia de mensajes en MQ](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="71bcb-180">Envío de un mensaje</span><span class="sxs-lookup"><span data-stu-id="71bcb-180">Send a message</span></span>
1. <span data-ttu-id="71bcb-181">Al agregar hello **enviar mensaje** acción, conexión primera Hola que está configurado de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="71bcb-181">When adding hello **Send message** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="71bcb-182">Seleccione **cambiar conexión** toocreate una conexión nueva, o seleccione otra conexión.</span><span class="sxs-lookup"><span data-stu-id="71bcb-182">Select **Change connection** toocreate a new connection, or select a different connection.</span></span> <span data-ttu-id="71bcb-183">Hola válido **tipos de mensaje** son **datagrama**, **respuesta**, o **solicitar**.</span><span class="sxs-lookup"><span data-stu-id="71bcb-183">hello valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="71bcb-184">![Propiedades de Send message](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="71bcb-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="71bcb-185">Hello salida del mensaje de envío Hola siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="71bcb-185">hello output of Send message looks like hello following:</span></span>  
![Salida de Send message](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="71bcb-187">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="71bcb-187">Connector-specific details</span></span>

<span data-ttu-id="71bcb-188">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/mq/).</span><span class="sxs-lookup"><span data-stu-id="71bcb-188">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="71bcb-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="71bcb-189">Next steps</span></span>
<span data-ttu-id="71bcb-190">[Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="71bcb-190">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="71bcb-191">Explorar Hola otros conectores disponibles en las aplicaciones lógicas en nuestro [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="71bcb-191">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
