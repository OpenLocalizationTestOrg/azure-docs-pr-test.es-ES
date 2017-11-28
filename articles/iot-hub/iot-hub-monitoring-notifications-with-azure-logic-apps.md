---
title: "supervisión remota de aaaIoT y notificaciones con las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Use las aplicaciones lógicas de Azure para la supervisión de temperatura de IoT en su centro de IoT y automáticamente enviar tooyour buzón de notificaciones de correo electrónico para cualquier anomalía que se ha detectado."
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
ms.openlocfilehash: 89396528ed63c37258e1b49f342f0723e686ecb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="c5b10-104">Supervisión remota y notificaciones de IoT con Azure Logic Apps conectando IoT Hub y el buzón de correo</span><span class="sxs-lookup"><span data-stu-id="c5b10-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="c5b10-106">Aplicaciones lógicas de Azure proporciona una manera de procesos de tooautomate como una serie de pasos.</span><span class="sxs-lookup"><span data-stu-id="c5b10-106">Azure Logic Apps provides a way tooautomate processes as a series of steps.</span></span> <span data-ttu-id="c5b10-107">Una aplicación lógica puede conectar diversos servicios y protocolos.</span><span class="sxs-lookup"><span data-stu-id="c5b10-107">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="c5b10-108">Comienza con un desencadenador como "Cuando se agregue una cuenta" y continúa con una combinación de acciones, una como "enviando una notificación de inserción".</span><span class="sxs-lookup"><span data-stu-id="c5b10-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="c5b10-109">Esta característica convierte a Logic Apps en una solución de IoT perfecta para la supervisión de IoT, por ejemplo, para mantenerse alerta en busca de anomalías, entre otros escenarios de uso.</span><span class="sxs-lookup"><span data-stu-id="c5b10-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="c5b10-110">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="c5b10-110">What you learn</span></span>

<span data-ttu-id="c5b10-111">Aprenderá cómo toocreate una aplicación de la lógica que se conecta el centro de IoT y el buzón para la supervisión de temperatura y notificaciones.</span><span class="sxs-lookup"><span data-stu-id="c5b10-111">You learn how toocreate a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="c5b10-112">Cuando la temperatura de hello es superior a 30 ° C, Hola marcas de aplicación de cliente `temperatureAlert = "true"` en mensajes de bienvenida envía tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c5b10-112">When hello temperature is above 30 C, hello client application marks `temperatureAlert = "true"` in hello message it sends tooyour IoT hub.</span></span> <span data-ttu-id="c5b10-113">mensaje de bienvenida de desencadenadores Hola toosend de aplicación lógica es una notificación de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="c5b10-113">hello message triggers hello logic app toosend you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="c5b10-114">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="c5b10-114">What you do</span></span>

* <span data-ttu-id="c5b10-115">Crear un espacio de nombres del bus de servicio y agregue un tooit de cola.</span><span class="sxs-lookup"><span data-stu-id="c5b10-115">Create a service bus namespace and add a queue tooit.</span></span>
* <span data-ttu-id="c5b10-116">Agregar un punto de conexión y un centro de IoT de enrutamiento regla tooyour.</span><span class="sxs-lookup"><span data-stu-id="c5b10-116">Add an endpoint and a routing rule tooyour IoT hub.</span></span>
* <span data-ttu-id="c5b10-117">Crear, configurar y probar una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="c5b10-117">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c5b10-118">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="c5b10-118">What you need</span></span>

* <span data-ttu-id="c5b10-119">Tutorial [configurar su dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completado donde abordan las Hola según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="c5b10-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  * <span data-ttu-id="c5b10-120">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="c5b10-120">An active Azure subscription.</span></span>
  * <span data-ttu-id="c5b10-121">Un centro de Azure IoT en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="c5b10-121">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="c5b10-122">Una aplicación de cliente que envía el centro de IoT de Azure de tooyour de mensajes.</span><span class="sxs-lookup"><span data-stu-id="c5b10-122">A client application that sends messages tooyour Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a><span data-ttu-id="c5b10-123">Crear espacio de nombres de bus de servicio y agregue un tooit de cola</span><span class="sxs-lookup"><span data-stu-id="c5b10-123">Create service bus namespace and add a queue tooit</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="c5b10-124">Crear un espacio de nombres de Service Bus</span><span class="sxs-lookup"><span data-stu-id="c5b10-124">Create a service bus namespace</span></span>

1. <span data-ttu-id="c5b10-125">En hello [portal de Azure](https://portal.azure.com/), haga clic en **New** > **integración empresarial** > **Bus de servicio**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-125">On hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="c5b10-126">Proporcionar Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="c5b10-126">Provide hello following information:</span></span>

   <span data-ttu-id="c5b10-127">**Nombre**: nombre de Hola Hola del bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="c5b10-127">**Name**: hello name of hello service bus.</span></span>

   <span data-ttu-id="c5b10-128">**Nivel de precios**: haga clic en **Básico** > **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-128">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="c5b10-129">nivel básico de Hello es suficiente para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c5b10-129">hello Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="c5b10-130">**Grupo de recursos**: Use Hola mismo grupo de recursos que usa el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c5b10-130">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="c5b10-131">**Ubicación**: Use Hola misma ubicación que utiliza el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c5b10-131">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="c5b10-132">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-132">Click **Create**.</span></span>

   ![Crear un espacio de nombres del bus de servicio en hello portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="c5b10-134">Agregar una cola de Service Bus</span><span class="sxs-lookup"><span data-stu-id="c5b10-134">Add a service bus queue</span></span>

1. <span data-ttu-id="c5b10-135">Abra el espacio de nombres del bus de servicio de hello y, a continuación, haga clic en **+ cola**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-135">Open hello service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="c5b10-136">Escriba un nombre para la cola de hello y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-136">Enter a name for hello queue and then click **Create**.</span></span>
1. <span data-ttu-id="c5b10-137">Abrir la cola de bus de servicio de hello y, a continuación, haga clic en **directivas de acceso compartido** > **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-137">Open hello service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="c5b10-138">Escriba un nombre para la directiva de hello, verificación **administrar**y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-138">Enter a name for hello policy, check **Manage**, and then click **Create**.</span></span>

   ![Agregar una cola de bus de servicio en hello portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a><span data-ttu-id="c5b10-140">Agregar un punto de conexión y un centro de IoT de enrutamiento regla tooyour</span><span class="sxs-lookup"><span data-stu-id="c5b10-140">Add an endpoint and a routing rule tooyour IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="c5b10-141">Agregación de un extremo</span><span class="sxs-lookup"><span data-stu-id="c5b10-141">Add an endpoint</span></span>

1. <span data-ttu-id="c5b10-142">Abra IoT Hub, haga clic en Puntos de conexión > + Agregar.</span><span class="sxs-lookup"><span data-stu-id="c5b10-142">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="c5b10-143">Escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="c5b10-143">Enter hello following information:</span></span>

   <span data-ttu-id="c5b10-144">**Nombre**: nombre de Hola de punto de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5b10-144">**Name**: hello name of hello endpoint.</span></span>

   <span data-ttu-id="c5b10-145">**Tipo de punto de conexión**: seleccione **Cola de Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-145">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="c5b10-146">**Espacio de nombres de Bus de servicio**: seleccione Hola espacio de nombres que creó.</span><span class="sxs-lookup"><span data-stu-id="c5b10-146">**Service Bus namespace**: Select hello namespace you created.</span></span>

   <span data-ttu-id="c5b10-147">**Cola de Service Bus**: cola de hello Select que ha creado.</span><span class="sxs-lookup"><span data-stu-id="c5b10-147">**Service Bus queue**: Select hello queue you created.</span></span>
1. <span data-ttu-id="c5b10-148">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-148">Click **OK**.</span></span>

   ![Agregar un centro de IoT de punto de conexión tooyour Hola portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="c5b10-150">Agregar una regla de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="c5b10-150">Add a routing rule</span></span>

1. <span data-ttu-id="c5b10-151">En IoT Hub, haga clic en **Rutas** > **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-151">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="c5b10-152">Escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="c5b10-152">Enter hello following information:</span></span>

   <span data-ttu-id="c5b10-153">**Nombre**: nombre de Hola de regla de enrutamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5b10-153">**Name**: hello name of hello routing rule.</span></span>

   <span data-ttu-id="c5b10-154">**Origen de datos**: seleccione **DeviceMessages**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-154">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="c5b10-155">**Punto de conexión**: seleccionar extremo Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="c5b10-155">**Endpoint**: Select hello endpoint you created.</span></span>

   <span data-ttu-id="c5b10-156">**Cadena de consulta**: escriba `temperatureAlert = "true"`.</span><span class="sxs-lookup"><span data-stu-id="c5b10-156">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="c5b10-157">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-157">Click **Save**.</span></span>

   ![Agregar una regla de enrutamiento de hello portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="c5b10-159">Crear y configurar una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="c5b10-159">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="c5b10-160">Creación de una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="c5b10-160">Create a logic app</span></span>

1. <span data-ttu-id="c5b10-161">Hola [portal de Azure](https://portal.azure.com/), haga clic en **New** > **integración empresarial** > **aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-161">In hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="c5b10-162">Escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="c5b10-162">Enter hello following information:</span></span>

   <span data-ttu-id="c5b10-163">**Nombre**: nombre de Hola de aplicación lógica de hello.</span><span class="sxs-lookup"><span data-stu-id="c5b10-163">**Name**: hello name of hello logic app.</span></span>

   <span data-ttu-id="c5b10-164">**Grupo de recursos**: Use Hola mismo grupo de recursos que usa el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c5b10-164">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="c5b10-165">**Ubicación**: Use Hola misma ubicación que utiliza el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c5b10-165">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="c5b10-166">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-166">Click **Create**.</span></span>

### <a name="configure-hello-logic-app"></a><span data-ttu-id="c5b10-167">Configurar la aplicación de la lógica de hello</span><span class="sxs-lookup"><span data-stu-id="c5b10-167">Configure hello logic app</span></span>

1. <span data-ttu-id="c5b10-168">Abra la aplicación de lógica de Hola que se abre en hello lógica el Diseñador de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c5b10-168">Open hello logic app that opens into hello Logic Apps Designer.</span></span>
1. <span data-ttu-id="c5b10-169">Hola lógica el Diseñador de aplicaciones, haga clic en **en blanco de lógica de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-169">In hello Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![Comenzar con una aplicación lógica en blanco en hello portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="c5b10-171">Haga clic en **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-171">Click **Service Bus**.</span></span>

   ![Seleccione toostart de Service Bus crear la aplicación lógica en hello portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="c5b10-173">Haga clic en **Service Bus: Cuando llegan uno o más mensajes a una cola (autocompletar)**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="c5b10-174">Cree una conexión de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="c5b10-174">Create a service bus connection.</span></span>
   1. <span data-ttu-id="c5b10-175">Escriba un nombre de conexión.</span><span class="sxs-lookup"><span data-stu-id="c5b10-175">Enter a connection name.</span></span>
   1. <span data-ttu-id="c5b10-176">Haga clic en el espacio de nombres del bus de servicio de hello > Hola directiva de bus de servicio > **crear**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-176">Click hello service bus namespace > hello service bus policy > **Create**.</span></span>

      ![Crear una conexión de bus de servicio para la aplicación lógica en hello portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="c5b10-178">Haga clic en **continuar** después de crean conexiones de bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5b10-178">Click **Continue** after hello service bus connection is created.</span></span>
   1. <span data-ttu-id="c5b10-179">Seleccione cola Hola que creó y escriba `175` para **recuento máximo de mensaje**</span><span class="sxs-lookup"><span data-stu-id="c5b10-179">Select hello queue that you created and enter `175` for **Maximum message count**</span></span>

      ![Especifique el número de máximo de los mensajes de Hola para conexiones de bus de servicio de hello en la aplicación lógica](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. <span data-ttu-id="c5b10-181">Haga clic en "Guardar" botón toosave Hola cambios.</span><span class="sxs-lookup"><span data-stu-id="c5b10-181">Click "Save" button toosave hello changes.</span></span>

1. <span data-ttu-id="c5b10-182">Cree una conexión de servicio SMTP.</span><span class="sxs-lookup"><span data-stu-id="c5b10-182">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="c5b10-183">Haga clic en **Nuevo paso** > **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-183">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="c5b10-184">Tipo de `SMTP`, haga clic en hello **SMTP** de servicio en el resultado de la búsqueda de hello y, a continuación, haga clic en **SMTP - enviar correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-184">Type `SMTP`, click hello **SMTP** service in hello search result, and then click **SMTP - Send Email**.</span></span>

      ![Crear una conexión de SMTP en la aplicación lógica en hello portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="c5b10-186">Escriba información de hello SMTP del buzón de correo y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-186">Enter hello SMTP information of your mailbox, and then click **Create**.</span></span>

      ![Escriba la información de conexión de SMTP en la aplicación lógica en hello portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="c5b10-188">Obtener información de hello SMTP de [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), y [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span><span class="sxs-lookup"><span data-stu-id="c5b10-188">Get hello SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="c5b10-189">Escriba la dirección de correo electrónico en **De** y **Para** y `High temperature detected` en **Asunto** y **Cuerpo**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="c5b10-190">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c5b10-190">Click **Save**.</span></span>

<span data-ttu-id="c5b10-191">aplicación de la lógica de Hello está en condiciones de funcionamiento cuando la guarde.</span><span class="sxs-lookup"><span data-stu-id="c5b10-191">hello logic app is in working order when you save it.</span></span>

## <a name="test-hello-logic-app"></a><span data-ttu-id="c5b10-192">Aplicación de prueba hello lógica</span><span class="sxs-lookup"><span data-stu-id="c5b10-192">Test hello logic app</span></span>

1. <span data-ttu-id="c5b10-193">Iniciar aplicación de cliente de Hola que implemente dispositivo tooyour en [ESP8266 conectar tooAzure centro de IoT](iot-hub-arduino-huzzah-esp8266-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c5b10-193">Start hello client application that you deploy tooyour device in [Connect ESP8266 tooAzure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="c5b10-194">Aumentar la temperatura del entorno de hello alrededor de hello SensorTag toobe superior a 30 C. Por ejemplo, claro una vela alrededor de su SensorTag.</span><span class="sxs-lookup"><span data-stu-id="c5b10-194">Increase hello environment temperature around hello SensorTag toobe above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="c5b10-195">Debería recibir una notificación por correo electrónico enviada por la aplicación de la lógica de hello.</span><span class="sxs-lookup"><span data-stu-id="c5b10-195">You should receive an email notification sent by hello logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c5b10-196">El proveedor de servicios de correo electrónico que necesite tooverify Hola remitente identidad toomake seguro es quién envía correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5b10-196">Your email service provider may need tooverify hello sender identity toomake sure it is you who sends hello email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5b10-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c5b10-197">Next steps</span></span>

<span data-ttu-id="c5b10-198">Ha creado correctamente una aplicación lógica que conecta IoT Hub y el buzón de correo para la supervisión de temperatura y las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="c5b10-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
