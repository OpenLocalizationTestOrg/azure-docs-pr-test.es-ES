---
title: aaaSave tooAzure el almacenamiento de datos de mensajes de su centro de IoT | Documentos de Microsoft
description: "Utilice un toosave de aplicación de Azure función su tooyour de mensajes del centro de IoT almacenamiento de tabla de Azure. mensajes de saludo IoT hub contienen información, como datos de sensor, que se envían desde el dispositivo de IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: almacenamiento de datos de iot, almacenamiento de datos del sensor de iot
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: be72d9ba9a781822926364351b50f58f5d96e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a><span data-ttu-id="fc74f-105">Guardar mensajes de centro de IoT que contienen el almacenamiento de tabla de Azure de sensor datos tooyour</span><span class="sxs-lookup"><span data-stu-id="fc74f-105">Save IoT hub messages that contain sensor data tooyour Azure table storage</span></span>

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="fc74f-107">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="fc74f-107">What you learn</span></span>

<span data-ttu-id="fc74f-108">Obtenga información acerca cómo toocreate una cuenta de almacenamiento de Azure y un Azure función mensajes de aplicación toostore IoT hub en el almacenamiento de tabla.</span><span class="sxs-lookup"><span data-stu-id="fc74f-108">You learn how toocreate an Azure storage account and an Azure function app toostore IoT hub messages in your table storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="fc74f-109">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="fc74f-109">What you do</span></span>

- <span data-ttu-id="fc74f-110">Cree una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="fc74f-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="fc74f-111">Prepare su centro de IoT los mensajes de tooread de conexión.</span><span class="sxs-lookup"><span data-stu-id="fc74f-111">Prepare your IoT hub connection tooread messages.</span></span>
- <span data-ttu-id="fc74f-112">Cree e implemente una aplicación de función de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc74f-112">Create and deploy an Azure function app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fc74f-113">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="fc74f-113">What you need</span></span>

- <span data-ttu-id="fc74f-114">[Configurar el dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) hello toocover según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="fc74f-114">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) toocover hello following requirements:</span></span>
  - <span data-ttu-id="fc74f-115">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="fc74f-115">An active Azure subscription</span></span>
  - <span data-ttu-id="fc74f-116">Una instancia de IoT Hub en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="fc74f-116">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="fc74f-117">Una aplicación en ejecución que envía el centro de IoT tooyour de mensajes</span><span class="sxs-lookup"><span data-stu-id="fc74f-117">A running application that sends messages tooyour IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="fc74f-118">Creación de una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="fc74f-118">Create an Azure storage account</span></span>

1. <span data-ttu-id="fc74f-119">Hola [portal de Azure](https://portal.azure.com/), haga clic en **New** > **almacenamiento** > **cuenta de almacenamiento**  >   **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-119">In hello [Azure portal](https://portal.azure.com/), click **New** > **Storage** > **Storage account** > **Create**.</span></span>

2. <span data-ttu-id="fc74f-120">Escriba información necesaria de Hola Hola cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="fc74f-120">Enter hello necessary information for hello storage account:</span></span>

   ![Crear una cuenta de almacenamiento en hello portal de Azure](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="fc74f-122">**Nombre**: nombre de Hola de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc74f-122">**Name**: hello name of hello storage account.</span></span> <span data-ttu-id="fc74f-123">nombre de Hello debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="fc74f-123">hello name must be globally unique.</span></span>

   * <span data-ttu-id="fc74f-124">**Grupo de recursos**: Use Hola mismo grupo de recursos que usa el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="fc74f-124">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="fc74f-125">**PIN toodashboard**: seleccione esta opción para el centro de IoT tooyour de fácil acceso desde el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc74f-125">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

3. <span data-ttu-id="fc74f-126">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-126">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a><span data-ttu-id="fc74f-127">Preparar su centro de IoT mensajes tooread la conexión.</span><span class="sxs-lookup"><span data-stu-id="fc74f-127">Prepare your IoT hub connection tooread messages</span></span>

<span data-ttu-id="fc74f-128">Centro de IoT muestra un punto de conexión compatible con el centro de eventos integrados de tooenable aplicaciones de tooread IoT de concentrador de mensajes.</span><span class="sxs-lookup"><span data-stu-id="fc74f-128">IoT hub exposes a built-in event hub-compatible endpoint tooenable applications tooread IoT hub messages.</span></span> <span data-ttu-id="fc74f-129">Mientras tanto, las aplicaciones usan datos de tooread de grupos de consumidor de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="fc74f-129">Meanwhile, applications use consumer groups tooread data from your IoT hub.</span></span> <span data-ttu-id="fc74f-130">Antes de crear un tooread de datos de aplicación de función Azure desde el centro de IoT, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="fc74f-130">Before you create an Azure function app tooread data from your IoT hub, do hello following:</span></span>

- <span data-ttu-id="fc74f-131">Obtener la cadena de conexión de Hola del extremo del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="fc74f-131">Get hello connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="fc74f-132">Crear un grupo de consumidores para el IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="fc74f-132">Create a consumer group for your IoT hub.</span></span>

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="fc74f-133">Obtener la cadena de conexión de Hola del extremo del centro de IoT</span><span class="sxs-lookup"><span data-stu-id="fc74f-133">Get hello connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="fc74f-134">Abra el IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="fc74f-134">Open your IoT hub.</span></span>

2. <span data-ttu-id="fc74f-135">En hello **centro de IoT** panel, en **mensajería**, haga clic en **extremos**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-135">On hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="fc74f-136">Hola haga panel, en **extremos integrados**, haga clic en **eventos**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-136">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="fc74f-137">Hola **propiedades** panel, Hola Nota siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="fc74f-137">In hello **Properties** pane, note hello following values:</span></span>
   - <span data-ttu-id="fc74f-138">Extremo compatible con Centro de eventos</span><span class="sxs-lookup"><span data-stu-id="fc74f-138">Event hub-compatible endpoint</span></span>
   - <span data-ttu-id="fc74f-139">Nombre compatible con Centro de eventos</span><span class="sxs-lookup"><span data-stu-id="fc74f-139">Event hub-compatible name</span></span>

   ![Obtener la cadena de conexión de Hola del extremo del centro de IoT Hola portal de Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. <span data-ttu-id="fc74f-141">Hola **centro de IoT** panel, en **configuración**, haga clic en **directivas de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-141">In hello **IoT Hub** pane, under **Settings**, click **Shared access policies**.</span></span>

6. <span data-ttu-id="fc74f-142">Haga clic en **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-142">Click **iothubowner**.</span></span>

7. <span data-ttu-id="fc74f-143">Hola Nota **clave principal** valor.</span><span class="sxs-lookup"><span data-stu-id="fc74f-143">Note hello **Primary key** value.</span></span>

8. <span data-ttu-id="fc74f-144">Cree la cadena de conexión de Hola del extremo del centro de IoT como sigue:</span><span class="sxs-lookup"><span data-stu-id="fc74f-144">Create hello connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > <span data-ttu-id="fc74f-145">Reemplace `<Event Hub-compatible endpoint>` y `<Primary key>` con valores de hello que anotó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fc74f-145">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with hello values that you noted earlier.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="fc74f-146">Crear un grupo de consumidores para el IoT Hub</span><span class="sxs-lookup"><span data-stu-id="fc74f-146">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="fc74f-147">Abra el IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="fc74f-147">Open your IoT hub.</span></span>

2. <span data-ttu-id="fc74f-148">Hola **centro de IoT** panel, en **mensajería**, haga clic en **extremos**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-148">In hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="fc74f-149">Hola haga panel, en **extremos integrados**, haga clic en **eventos**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-149">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="fc74f-150">Hola **propiedades** panel, en **grupos de consumidores**, escriba un nombre y, a continuación, tome nota del mismo.</span><span class="sxs-lookup"><span data-stu-id="fc74f-150">In hello **Properties** pane, under **Consumer groups**, enter a name, and then make a note of it.</span></span>

5. <span data-ttu-id="fc74f-151">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-151">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="fc74f-152">Creación e implementación de una aplicación de función de Azure</span><span class="sxs-lookup"><span data-stu-id="fc74f-152">Create and deploy an Azure function app</span></span>

1. <span data-ttu-id="fc74f-153">Hola [portal de Azure](https://portal.azure.com/), haga clic en **New** > **proceso** > **aplicación de la función**  >   **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-153">In hello [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App** > **Create**.</span></span>

2. <span data-ttu-id="fc74f-154">Escriba la información necesaria de hello para la aplicación de la función de hello.</span><span class="sxs-lookup"><span data-stu-id="fc74f-154">Enter hello necessary information for hello function app.</span></span>

   ![Crear una aplicación de la función en hello portal de Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * <span data-ttu-id="fc74f-156">**Nombre de la aplicación**: nombre de Hola de aplicación de la función de hello.</span><span class="sxs-lookup"><span data-stu-id="fc74f-156">**App name**: hello name of hello function app.</span></span> <span data-ttu-id="fc74f-157">nombre de Hello debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="fc74f-157">hello name must be globally unique.</span></span>

   * <span data-ttu-id="fc74f-158">**Grupo de recursos**: Use Hola mismo grupo de recursos que usa el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="fc74f-158">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="fc74f-159">**Cuenta de almacenamiento**: Hola cuenta de almacenamiento que ha creado.</span><span class="sxs-lookup"><span data-stu-id="fc74f-159">**Storage Account**: hello storage account that you created.</span></span>

   * <span data-ttu-id="fc74f-160">**PIN toodashboard**: Active esta opción para facilitar el acceso toohello función aplicación de panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc74f-160">**Pin toodashboard**: Check this option for easy access toohello function app from hello dashboard.</span></span>

3. <span data-ttu-id="fc74f-161">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-161">Click **Create**.</span></span>

4. <span data-ttu-id="fc74f-162">Una vez creada la aplicación de la función de hello, ábralo.</span><span class="sxs-lookup"><span data-stu-id="fc74f-162">After hello function app has been created, open it.</span></span>

5. <span data-ttu-id="fc74f-163">En la aplicación de la función de hello, cree una nueva función haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="fc74f-163">In hello function app, create a new function by doing hello following:</span></span>

   <span data-ttu-id="fc74f-164">a.</span><span class="sxs-lookup"><span data-stu-id="fc74f-164">a.</span></span> <span data-ttu-id="fc74f-165">Haga clic en **Nueva función**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-165">Click **New Function**.</span></span>

   <span data-ttu-id="fc74f-166">b.</span><span class="sxs-lookup"><span data-stu-id="fc74f-166">b.</span></span> <span data-ttu-id="fc74f-167">Seleccione **JavaScript** para **Lenguaje** y **Procesamiento de datos** para **Escenario**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-167">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>

   <span data-ttu-id="fc74f-168">c.</span><span class="sxs-lookup"><span data-stu-id="fc74f-168">c.</span></span> <span data-ttu-id="fc74f-169">Haga clic en **Crear esta función** y en **Nueva función**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-169">Click **Create this function**, and then click **New Function**.</span></span>

   <span data-ttu-id="fc74f-170">d.</span><span class="sxs-lookup"><span data-stu-id="fc74f-170">d.</span></span> <span data-ttu-id="fc74f-171">Seleccione **JavaScript** para el idioma de hello, y **procesamiento de datos** para el escenario de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc74f-171">Select **JavaScript** for hello language, and **Data Processing** for hello scenario.</span></span>

   <span data-ttu-id="fc74f-172">e.</span><span class="sxs-lookup"><span data-stu-id="fc74f-172">e.</span></span> <span data-ttu-id="fc74f-173">Haga clic en hello **EventHubTrigger JavaScript** plantilla.</span><span class="sxs-lookup"><span data-stu-id="fc74f-173">Click hello **EventHubTrigger-JavaScript** template.</span></span>

   <span data-ttu-id="fc74f-174">f.</span><span class="sxs-lookup"><span data-stu-id="fc74f-174">f.</span></span> <span data-ttu-id="fc74f-175">Escriba Hola información necesaria para la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc74f-175">Enter hello necessary information for hello template.</span></span>

      * <span data-ttu-id="fc74f-176">**Nombre de la función**: nombre de Hola de función hello.</span><span class="sxs-lookup"><span data-stu-id="fc74f-176">**Name your function**: hello name of hello function.</span></span>

      * <span data-ttu-id="fc74f-177">**Nombre del concentrador de eventos**: nombre de compatible con el concentrador de eventos de Hola que anotó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fc74f-177">**Event Hub name**: hello event hub-compatible name that you noted earlier.</span></span>

      * <span data-ttu-id="fc74f-178">**Conexión de concentrador de eventos**: cadena de conexión de hello tooadd de extremo del centro de IoT Hola que ha creado, haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-178">**Event Hub connection**: tooadd hello connection string of hello IoT hub endpoint that you created, click **New**.</span></span>

   <span data-ttu-id="fc74f-179">g.</span><span class="sxs-lookup"><span data-stu-id="fc74f-179">g.</span></span> <span data-ttu-id="fc74f-180">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-180">Click **Create**.</span></span>

6. <span data-ttu-id="fc74f-181">Configurar una salida de función hello haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="fc74f-181">Configure an output of hello function by doing hello following:</span></span>

   <span data-ttu-id="fc74f-182">a.</span><span class="sxs-lookup"><span data-stu-id="fc74f-182">a.</span></span> <span data-ttu-id="fc74f-183">Haga clic en **Integrar** > **Nueva salida** > **Azure Table Storage** > **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-183">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![Agregar tabla almacenamiento tooyour función aplicación Hola portal de Azure](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   <span data-ttu-id="fc74f-185">b.</span><span class="sxs-lookup"><span data-stu-id="fc74f-185">b.</span></span> <span data-ttu-id="fc74f-186">Escriba la información necesaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc74f-186">Enter hello necessary information.</span></span>

      * <span data-ttu-id="fc74f-187">**Nombre de parámetro de tabla**: Use `outputTable`, que se utilizarán en hello Azure código de la función.</span><span class="sxs-lookup"><span data-stu-id="fc74f-187">**Table parameter name**: Use `outputTable`, which will be used in hello Azure function's code.</span></span>
      
      * <span data-ttu-id="fc74f-188">**Nombre de la tabla**: use `deviceData`.</span><span class="sxs-lookup"><span data-stu-id="fc74f-188">**Table name**: Use `deviceData`.</span></span>

      * <span data-ttu-id="fc74f-189">**Conexión de cuenta de Storage**: haga clic en **Nuevo** y seleccione o escriba la cuenta de Storage.</span><span class="sxs-lookup"><span data-stu-id="fc74f-189">**Storage account connection**: Click **New**, and then select or enter your storage account.</span></span> <span data-ttu-id="fc74f-190">Si no se muestra la cuenta de almacenamiento de hello, consulte [requisitos de la cuenta de almacenamiento](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="fc74f-190">If hello storage account is not displayed, see [Storage account requirements](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span></span>
      
   <span data-ttu-id="fc74f-191">c.</span><span class="sxs-lookup"><span data-stu-id="fc74f-191">c.</span></span> <span data-ttu-id="fc74f-192">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-192">Click **Save**.</span></span>

7. <span data-ttu-id="fc74f-193">En **Desencadenadores**, haga clic en **Azure Event Hubs (eventHubMessages)**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-193">Under **Triggers**, click **Azure Event Hub (eventHubMessages)**.</span></span>

8. <span data-ttu-id="fc74f-194">En **grupo de consumidores del centro de eventos**, escriba Hola nombre de grupo de consumidores de Hola que creó y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-194">Under **Event Hub consumer group**, enter hello name of hello consumer group that you created, and then click **Save**.</span></span>

9. <span data-ttu-id="fc74f-195">Haga clic en función de Hola que haya creado en hello izquierda y, a continuación, haga clic en **ver archivos** en hello derecho.</span><span class="sxs-lookup"><span data-stu-id="fc74f-195">Click hello function you've created on hello left and then click **View Files** on hello right.</span></span>

10. <span data-ttu-id="fc74f-196">Reemplace el código de hello en `index.js` con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="fc74f-196">Replace hello code in `index.js` with hello following:</span></span>

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in hello IoT hub.
   // hello message payload is persisted in an Azure storage table
 
   module.exports = function (context, iotHubMessage) {
    context.log('Message received: ' + JSON.stringify(iotHubMessage));
    var date = Date.now();
    var partitionKey = Math.floor(date / (24 * 60 * 60 * 1000)) + '';
    var rowKey = date + '';
    context.bindings.outputTable = {
     "partitionKey": partitionKey,
     "rowKey": rowKey,
     "message": JSON.stringify(iotHubMessage)
    };
    context.done();
   };
   ```

11. <span data-ttu-id="fc74f-197">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-197">Click **Save**.</span></span>

<span data-ttu-id="fc74f-198">Ahora ha creado la aplicación de la función de hello.</span><span class="sxs-lookup"><span data-stu-id="fc74f-198">You have now created hello function app.</span></span> <span data-ttu-id="fc74f-199">que almacena mensajes que la instancia de IoT Hub recibe en Table Storage.</span><span class="sxs-lookup"><span data-stu-id="fc74f-199">It stores messages that your IoT hub receives in your table storage.</span></span>

> [!NOTE]
> <span data-ttu-id="fc74f-200">Puede usar hello **ejecutar** aplicación de función de botón tootest hello.</span><span class="sxs-lookup"><span data-stu-id="fc74f-200">You can use hello **Run** button tootest hello function app.</span></span> <span data-ttu-id="fc74f-201">Al hacer clic en **ejecutar**, se envía el mensaje de prueba de hello tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="fc74f-201">When you click **Run**, hello test message is sent tooyour IoT hub.</span></span> <span data-ttu-id="fc74f-202">llegada Hola de mensaje de bienvenida de debe desencadenar Hola función aplicación toostart y, a continuación, guarde el almacenamiento de tabla de tooyour mensaje Hola.</span><span class="sxs-lookup"><span data-stu-id="fc74f-202">hello arrival of hello message should trigger hello function app toostart and then save hello message tooyour table storage.</span></span> <span data-ttu-id="fc74f-203">Hola **registros** panel registra los detalles de hello del proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc74f-203">hello **Logs** pane records hello details of hello process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="fc74f-204">Comprobación del mensaje en Table Storage</span><span class="sxs-lookup"><span data-stu-id="fc74f-204">Verify your message in your table storage</span></span>

1. <span data-ttu-id="fc74f-205">Ejecutar la aplicación de ejemplo de Hola en su centro de IoT de dispositivo toosend mensajes tooyour.</span><span class="sxs-lookup"><span data-stu-id="fc74f-205">Run hello sample application on your device toosend messages tooyour IoT hub.</span></span>

2. <span data-ttu-id="fc74f-206">[Descargue e instale el Explorador de Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="fc74f-206">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="fc74f-207">Abra el Explorador de almacenamiento, haga clic en **agregar una cuenta de Azure** > **iniciar sesión en**y, a continuación, inicie sesión en tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc74f-207">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in tooyour Azure account.</span></span>

4. <span data-ttu-id="fc74f-208">Haga clic en la suscripción de Azure > **Cuentas de almacenamiento** > su cuenta de almacenamiento > **Tablas** > **deviceData**.</span><span class="sxs-lookup"><span data-stu-id="fc74f-208">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="fc74f-209">Debería ver los mensajes enviados desde el centro de IoT de tooyour dispositivos registrado en hello `deviceData` tabla.</span><span class="sxs-lookup"><span data-stu-id="fc74f-209">You should see messages sent from your device tooyour IoT hub logged in hello `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc74f-210">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fc74f-210">Next steps</span></span>

<span data-ttu-id="fc74f-211">Ha creado correctamente la cuenta de Azure Storage y la aplicación de función de Azure, donde se almacenan los mensajes que recibe la instancia de IoT Hub de Table Storage.</span><span class="sxs-lookup"><span data-stu-id="fc74f-211">You’ve successfully created your Azure storage account and Azure function app, which stores messages that your IoT hub receives in your table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
