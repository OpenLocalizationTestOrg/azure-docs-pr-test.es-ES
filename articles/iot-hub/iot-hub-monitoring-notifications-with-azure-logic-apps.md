---
title: "Supervisión remota y notificaciones de IoT con Azure Logic Apps | Microsoft Docs"
description: "Use Azure Logic Apps para la supervisión de temperatura de IoT en IoT Hub y el envío automático de notificaciones de correo electrónico al buzón de correo cada vez que se detecten anomalías."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "supervisión de iot, notificaciones de iot, supervisión de temperatura de iot"
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 7a611912ae55eb22103539dbba9f1a06aaa543b7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="5adc8-104">Supervisión remota y notificaciones de IoT con Azure Logic Apps conectando IoT Hub y el buzón de correo</span><span class="sxs-lookup"><span data-stu-id="5adc8-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="5adc8-106">Azure Logic Apps proporciona una manera de automatizar los procesos como una serie de pasos.</span><span class="sxs-lookup"><span data-stu-id="5adc8-106">Azure Logic Apps provides a way to automate processes as a series of steps.</span></span> <span data-ttu-id="5adc8-107">Una aplicación lógica puede conectar diversos servicios y protocolos.</span><span class="sxs-lookup"><span data-stu-id="5adc8-107">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="5adc8-108">Comienza con un desencadenador como "Cuando se agregue una cuenta" y continúa con una combinación de acciones, una como "enviando una notificación de inserción".</span><span class="sxs-lookup"><span data-stu-id="5adc8-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="5adc8-109">Esta característica convierte a Logic Apps en una solución de IoT perfecta para la supervisión de IoT, por ejemplo, para mantenerse alerta en busca de anomalías, entre otros escenarios de uso.</span><span class="sxs-lookup"><span data-stu-id="5adc8-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="5adc8-110">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="5adc8-110">What you learn</span></span>

<span data-ttu-id="5adc8-111">Aprenda a crear una aplicación lógica que conecte IoT Hub y el buzón de correo para la supervisión de temperatura y las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="5adc8-111">You learn how to create a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="5adc8-112">Cuando la temperatura es superior a 30 °C, la aplicación cliente marca `temperatureAlert = "true"` en el mensaje que envía a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5adc8-112">When the temperature is above 30 C, the client application marks `temperatureAlert = "true"` in the message it sends to your IoT hub.</span></span> <span data-ttu-id="5adc8-113">El mensaje desencadena la aplicación lógica para enviar una notificación de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="5adc8-113">The message triggers the logic app to send you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="5adc8-114">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="5adc8-114">What you do</span></span>

* <span data-ttu-id="5adc8-115">Crear un espacio de nombres de Service Bus y agregarle una cola.</span><span class="sxs-lookup"><span data-stu-id="5adc8-115">Create a service bus namespace and add a queue to it.</span></span>
* <span data-ttu-id="5adc8-116">Agregar un punto de conexión y una regla de enrutamiento a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5adc8-116">Add an endpoint and a routing rule to your IoT hub.</span></span>
* <span data-ttu-id="5adc8-117">Crear, configurar y probar una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="5adc8-117">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5adc8-118">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="5adc8-118">What you need</span></span>

* <span data-ttu-id="5adc8-119">Tutorial [Instalación de su dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completado donde se abordan los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="5adc8-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  * <span data-ttu-id="5adc8-120">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="5adc8-120">An active Azure subscription.</span></span>
  * <span data-ttu-id="5adc8-121">Un centro de Azure IoT en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="5adc8-121">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="5adc8-122">Una aplicación cliente que envía mensajes a su centro de Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="5adc8-122">A client application that sends messages to your Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-to-it"></a><span data-ttu-id="5adc8-123">Crear un espacio de nombres de Service Bus y agregarle una cola</span><span class="sxs-lookup"><span data-stu-id="5adc8-123">Create service bus namespace and add a queue to it</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="5adc8-124">Crear un espacio de nombres de Service Bus</span><span class="sxs-lookup"><span data-stu-id="5adc8-124">Create a service bus namespace</span></span>

1. <span data-ttu-id="5adc8-125">En [Azure Portal](https://portal.azure.com/), haga clic en **Nuevo** > **Enterprise Integration** > **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-125">On the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="5adc8-126">Proporcione la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="5adc8-126">Provide the following information:</span></span>

   <span data-ttu-id="5adc8-127">**Nombre**: nombre de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="5adc8-127">**Name**: The name of the service bus.</span></span>

   <span data-ttu-id="5adc8-128">**Nivel de precios**: haga clic en **Básico** > **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-128">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="5adc8-129">El nivel Básico es suficiente para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="5adc8-129">The Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="5adc8-130">**Grupo de recursos**: use el mismo grupo de recursos que usa el IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5adc8-130">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="5adc8-131">**Ubicación**: use la misma ubicación que emplea IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5adc8-131">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="5adc8-132">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-132">Click **Create**.</span></span>

   ![Crear un espacio de nombres de Service Bus en Azure Portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="5adc8-134">Agregar una cola de Service Bus</span><span class="sxs-lookup"><span data-stu-id="5adc8-134">Add a service bus queue</span></span>

1. <span data-ttu-id="5adc8-135">Abra el espacio de nombres de Service Bus y haga clic en **+ Cola**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-135">Open the service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="5adc8-136">Escriba un nombre para la cola y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-136">Enter a name for the queue and then click **Create**.</span></span>
1. <span data-ttu-id="5adc8-137">Abra la cola de Service Bus y haga clic en **Directivas de acceso compartido** > **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-137">Open the service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="5adc8-138">Escriba un nombre para la directiva, active **Administrar** y luego haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-138">Enter a name for the policy, check **Manage**, and then click **Create**.</span></span>

   ![Agregar una cola de Service Bus en Azure Portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-to-your-iot-hub"></a><span data-ttu-id="5adc8-140">Agregar un punto de conexión y una regla de enrutamiento a IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5adc8-140">Add an endpoint and a routing rule to your IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="5adc8-141">Agregación de un extremo</span><span class="sxs-lookup"><span data-stu-id="5adc8-141">Add an endpoint</span></span>

1. <span data-ttu-id="5adc8-142">Abra IoT Hub, haga clic en Puntos de conexión > + Agregar.</span><span class="sxs-lookup"><span data-stu-id="5adc8-142">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="5adc8-143">Escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="5adc8-143">Enter the following information:</span></span>

   <span data-ttu-id="5adc8-144">**Nombre**: nombre del punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="5adc8-144">**Name**: The name of the endpoint.</span></span>

   <span data-ttu-id="5adc8-145">**Tipo de punto de conexión**: seleccione **Cola de Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-145">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="5adc8-146">**Espacio de nombres de Service Bus**: seleccione el espacio de nombres que ha creado.</span><span class="sxs-lookup"><span data-stu-id="5adc8-146">**Service Bus namespace**: Select the namespace you created.</span></span>

   <span data-ttu-id="5adc8-147">**Cola de Service Bus**: seleccione la cola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="5adc8-147">**Service Bus queue**: Select the queue you created.</span></span>
1. <span data-ttu-id="5adc8-148">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-148">Click **OK**.</span></span>

   ![Agregar un punto de conexión a IoT Hub en Azure Portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="5adc8-150">Agregar una regla de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="5adc8-150">Add a routing rule</span></span>

1. <span data-ttu-id="5adc8-151">En IoT Hub, haga clic en **Rutas** > **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-151">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="5adc8-152">Escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="5adc8-152">Enter the following information:</span></span>

   <span data-ttu-id="5adc8-153">**Nombre**: nombre de la regla de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="5adc8-153">**Name**: The name of the routing rule.</span></span>

   <span data-ttu-id="5adc8-154">**Origen de datos**: seleccione **DeviceMessages**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-154">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="5adc8-155">**Punto de conexión**: seleccione el punto de conexión que ha creado.</span><span class="sxs-lookup"><span data-stu-id="5adc8-155">**Endpoint**: Select the endpoint you created.</span></span>

   <span data-ttu-id="5adc8-156">**Cadena de consulta**: escriba `temperatureAlert = "true"`.</span><span class="sxs-lookup"><span data-stu-id="5adc8-156">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="5adc8-157">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-157">Click **Save**.</span></span>

   ![Agregar una regla de enrutamiento en Azure Portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="5adc8-159">Crear y configurar una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="5adc8-159">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="5adc8-160">Creación de una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="5adc8-160">Create a logic app</span></span>

1. <span data-ttu-id="5adc8-161">En [Azure Portal](https://portal.azure.com/), haga clic en **Nuevo** > **Enterprise Integration** > **Aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-161">In the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="5adc8-162">Escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="5adc8-162">Enter the following information:</span></span>

   <span data-ttu-id="5adc8-163">**Nombre**: nombre de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="5adc8-163">**Name**: The name of the logic app.</span></span>

   <span data-ttu-id="5adc8-164">**Grupo de recursos**: use el mismo grupo de recursos que usa el IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5adc8-164">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="5adc8-165">**Ubicación**: use la misma ubicación que emplea IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5adc8-165">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="5adc8-166">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-166">Click **Create**.</span></span>

### <a name="configure-the-logic-app"></a><span data-ttu-id="5adc8-167">Configurar la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="5adc8-167">Configure the logic app</span></span>

1. <span data-ttu-id="5adc8-168">Abra la aplicación lógica que se abre en el Diseñador de aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="5adc8-168">Open the logic app that opens into the Logic Apps Designer.</span></span>
1. <span data-ttu-id="5adc8-169">En el Diseñador de aplicaciones lógicas, haga clic en **Aplicación lógica en blanco**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-169">In the Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![Comenzar con una aplicación lógica en blanco en Azure Portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="5adc8-171">Haga clic en **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-171">Click **Service Bus**.</span></span>

   ![Seleccionar Service Bus para empezar a crear la aplicación lógica en Azure Portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="5adc8-173">Haga clic en **Service Bus: Cuando llegan uno o más mensajes a una cola (autocompletar)**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="5adc8-174">Cree una conexión de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="5adc8-174">Create a service bus connection.</span></span>
   1. <span data-ttu-id="5adc8-175">Escriba un nombre de conexión.</span><span class="sxs-lookup"><span data-stu-id="5adc8-175">Enter a connection name.</span></span>
   1. <span data-ttu-id="5adc8-176">Haga clic en el espacio de nombres de Service Bus > directiva de Service Bus > **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-176">Click the service bus namespace > the service bus policy > **Create**.</span></span>

      ![Crear una conexión de Service Bus para la aplicación lógica en Azure Portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="5adc8-178">Haga clic en **Continuar** después de crear la conexión de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="5adc8-178">Click **Continue** after the service bus connection is created.</span></span>
   1. <span data-ttu-id="5adc8-179">Seleccione la cola que ha creado y escriba `175` en **Recuento máximo de mensajes**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-179">Select the queue that you created and enter `175` for **Maximum message count**</span></span>

      ![Especificar el recuento máximo de mensajes de la conexión de Service Bus en la aplicación lógica](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. <span data-ttu-id="5adc8-181">Haga clic en el botón "Guardar" para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="5adc8-181">Click "Save" button to save the changes.</span></span>

1. <span data-ttu-id="5adc8-182">Cree una conexión de servicio SMTP.</span><span class="sxs-lookup"><span data-stu-id="5adc8-182">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="5adc8-183">Haga clic en **Nuevo paso** > **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-183">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="5adc8-184">Escriba `SMTP`, haga clic en el servicio **SMTP** en el resultado de la búsqueda y luego haga clic en **SMTP: Enviar correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-184">Type `SMTP`, click the **SMTP** service in the search result, and then click **SMTP - Send Email**.</span></span>

      ![Crear una conexión SMTP en la aplicación lógica en Azure Portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="5adc8-186">Escriba la información SMTP del buzón de correo y luego haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-186">Enter the SMTP information of your mailbox, and then click **Create**.</span></span>

      ![Escribir la información de la conexión SMTP en la aplicación lógica en Azure Portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="5adc8-188">Obtenga la información SMTP de [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en) y [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span><span class="sxs-lookup"><span data-stu-id="5adc8-188">Get the SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="5adc8-189">Escriba la dirección de correo electrónico en **De** y **Para** y `High temperature detected` en **Asunto** y **Cuerpo**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="5adc8-190">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="5adc8-190">Click **Save**.</span></span>

<span data-ttu-id="5adc8-191">La aplicación lógica está funcionando al guardarse.</span><span class="sxs-lookup"><span data-stu-id="5adc8-191">The logic app is in working order when you save it.</span></span>

## <a name="test-the-logic-app"></a><span data-ttu-id="5adc8-192">Probar la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="5adc8-192">Test the logic app</span></span>

1. <span data-ttu-id="5adc8-193">Inicie la aplicación cliente que se implementa en el dispositivo en [Connect ESP8266 to Azure IoT Hub (Conectar ESP8266 a Azure IoT Hub)](iot-hub-arduino-huzzah-esp8266-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5adc8-193">Start the client application that you deploy to your device in [Connect ESP8266 to Azure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="5adc8-194">Aumente la temperatura ambiental en torno al SensorTag para que sea superior a 30 °C. Por ejemplo, encienda una vela al lado del SensorTag.</span><span class="sxs-lookup"><span data-stu-id="5adc8-194">Increase the environment temperature around the SensorTag to be above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="5adc8-195">Debería recibir una notificación de correo electrónico enviada por la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="5adc8-195">You should receive an email notification sent by the logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5adc8-196">Es posible que el proveedor de servicios de correo electrónico necesite comprobar la identidad del remitente para asegurarse de que es usted quien envía el mensaje.</span><span class="sxs-lookup"><span data-stu-id="5adc8-196">Your email service provider may need to verify the sender identity to make sure it is you who sends the email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5adc8-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5adc8-197">Next steps</span></span>

<span data-ttu-id="5adc8-198">Ha creado correctamente una aplicación lógica que conecta IoT Hub y el buzón de correo para la supervisión de temperatura y las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="5adc8-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
