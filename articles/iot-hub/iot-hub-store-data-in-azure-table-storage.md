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
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a>Guardar mensajes de centro de IoT que contienen el almacenamiento de tabla de Azure de sensor datos tooyour

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Conocimientos que adquirirá

Obtenga información acerca cómo toocreate una cuenta de almacenamiento de Azure y un Azure función mensajes de aplicación toostore IoT hub en el almacenamiento de tabla.

## <a name="what-you-do"></a>Qué debe hacer

- Cree una cuenta de Azure Storage.
- Prepare su centro de IoT los mensajes de tooread de conexión.
- Cree e implemente una aplicación de función de Azure.

## <a name="what-you-need"></a>Lo que necesita

- [Configurar el dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) hello toocover según los requisitos:
  - Una suscripción de Azure activa.
  - Una instancia de IoT Hub en su suscripción. 
  - Una aplicación en ejecución que envía el centro de IoT tooyour de mensajes

## <a name="create-an-azure-storage-account"></a>Creación de una cuenta de Azure Storage

1. Hola [portal de Azure](https://portal.azure.com/), haga clic en **New** > **almacenamiento** > **cuenta de almacenamiento**  >   **Crear**.

2. Escriba información necesaria de Hola Hola cuenta de almacenamiento:

   ![Crear una cuenta de almacenamiento en hello portal de Azure](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * **Nombre**: nombre de Hola de cuenta de almacenamiento de Hola. nombre de Hello debe ser único globalmente.

   * **Grupo de recursos**: Use Hola mismo grupo de recursos que usa el centro de IoT.

   * **PIN toodashboard**: seleccione esta opción para el centro de IoT tooyour de fácil acceso desde el panel de Hola.

3. Haga clic en **Crear**.

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a>Preparar su centro de IoT mensajes tooread la conexión.

Centro de IoT muestra un punto de conexión compatible con el centro de eventos integrados de tooenable aplicaciones de tooread IoT de concentrador de mensajes. Mientras tanto, las aplicaciones usan datos de tooread de grupos de consumidor de su centro de IoT. Antes de crear un tooread de datos de aplicación de función Azure desde el centro de IoT, Hola siguientes:

- Obtener la cadena de conexión de Hola del extremo del centro de IoT.
- Crear un grupo de consumidores para el IoT Hub.

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a>Obtener la cadena de conexión de Hola del extremo del centro de IoT

1. Abra el IoT Hub.

2. En hello **centro de IoT** panel, en **mensajería**, haga clic en **extremos**.

3. Hola haga panel, en **extremos integrados**, haga clic en **eventos**.

4. Hola **propiedades** panel, Hola Nota siguientes valores:
   - Extremo compatible con Centro de eventos
   - Nombre compatible con Centro de eventos

   ![Obtener la cadena de conexión de Hola del extremo del centro de IoT Hola portal de Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. Hola **centro de IoT** panel, en **configuración**, haga clic en **directivas de acceso compartido**.

6. Haga clic en **iothubowner**.

7. Hola Nota **clave principal** valor.

8. Cree la cadena de conexión de Hola del extremo del centro de IoT como sigue:

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > Reemplace `<Event Hub-compatible endpoint>` y `<Primary key>` con valores de hello que anotó anteriormente.

### <a name="create-a-consumer-group-for-your-iot-hub"></a>Crear un grupo de consumidores para el IoT Hub

1. Abra el IoT Hub.

2. Hola **centro de IoT** panel, en **mensajería**, haga clic en **extremos**.

3. Hola haga panel, en **extremos integrados**, haga clic en **eventos**.

4. Hola **propiedades** panel, en **grupos de consumidores**, escriba un nombre y, a continuación, tome nota del mismo.

5. Haga clic en **Guardar**.

## <a name="create-and-deploy-an-azure-function-app"></a>Creación e implementación de una aplicación de función de Azure

1. Hola [portal de Azure](https://portal.azure.com/), haga clic en **New** > **proceso** > **aplicación de la función**  >   **Crear**.

2. Escriba la información necesaria de hello para la aplicación de la función de hello.

   ![Crear una aplicación de la función en hello portal de Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * **Nombre de la aplicación**: nombre de Hola de aplicación de la función de hello. nombre de Hello debe ser único globalmente.

   * **Grupo de recursos**: Use Hola mismo grupo de recursos que usa el centro de IoT.

   * **Cuenta de almacenamiento**: Hola cuenta de almacenamiento que ha creado.

   * **PIN toodashboard**: Active esta opción para facilitar el acceso toohello función aplicación de panel de Hola.

3. Haga clic en **Crear**.

4. Una vez creada la aplicación de la función de hello, ábralo.

5. En la aplicación de la función de hello, cree una nueva función haciendo Hola siguiente:

   a. Haga clic en **Nueva función**.

   b. Seleccione **JavaScript** para **Lenguaje** y **Procesamiento de datos** para **Escenario**.

   c. Haga clic en **Crear esta función** y en **Nueva función**.

   d. Seleccione **JavaScript** para el idioma de hello, y **procesamiento de datos** para el escenario de Hola.

   e. Haga clic en hello **EventHubTrigger JavaScript** plantilla.

   f. Escriba Hola información necesaria para la plantilla de Hola.

      * **Nombre de la función**: nombre de Hola de función hello.

      * **Nombre del concentrador de eventos**: nombre de compatible con el concentrador de eventos de Hola que anotó anteriormente.

      * **Conexión de concentrador de eventos**: cadena de conexión de hello tooadd de extremo del centro de IoT Hola que ha creado, haga clic en **nuevo**.

   g. Haga clic en **Crear**.

6. Configurar una salida de función hello haciendo Hola siguiente:

   a. Haga clic en **Integrar** > **Nueva salida** > **Azure Table Storage** > **Seleccionar**.

      ![Agregar tabla almacenamiento tooyour función aplicación Hola portal de Azure](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   b. Escriba la información necesaria de Hola.

      * **Nombre de parámetro de tabla**: Use `outputTable`, que se utilizarán en hello Azure código de la función.
      
      * **Nombre de la tabla**: use `deviceData`.

      * **Conexión de cuenta de Storage**: haga clic en **Nuevo** y seleccione o escriba la cuenta de Storage. Si no se muestra la cuenta de almacenamiento de hello, consulte [requisitos de la cuenta de almacenamiento](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).
      
   c. Haga clic en **Guardar**.

7. En **Desencadenadores**, haga clic en **Azure Event Hubs (eventHubMessages)**.

8. En **grupo de consumidores del centro de eventos**, escriba Hola nombre de grupo de consumidores de Hola que creó y, a continuación, haga clic en **guardar**.

9. Haga clic en función de Hola que haya creado en hello izquierda y, a continuación, haga clic en **ver archivos** en hello derecho.

10. Reemplace el código de hello en `index.js` con siguiente hello:

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

11. Haga clic en **Guardar**.

Ahora ha creado la aplicación de la función de hello. que almacena mensajes que la instancia de IoT Hub recibe en Table Storage.

> [!NOTE]
> Puede usar hello **ejecutar** aplicación de función de botón tootest hello. Al hacer clic en **ejecutar**, se envía el mensaje de prueba de hello tooyour centro de IoT. llegada Hola de mensaje de bienvenida de debe desencadenar Hola función aplicación toostart y, a continuación, guarde el almacenamiento de tabla de tooyour mensaje Hola. Hola **registros** panel registra los detalles de hello del proceso de Hola.

## <a name="verify-your-message-in-your-table-storage"></a>Comprobación del mensaje en Table Storage

1. Ejecutar la aplicación de ejemplo de Hola en su centro de IoT de dispositivo toosend mensajes tooyour.

2. [Descargue e instale el Explorador de Azure Storage](http://storageexplorer.com/).

3. Abra el Explorador de almacenamiento, haga clic en **agregar una cuenta de Azure** > **iniciar sesión en**y, a continuación, inicie sesión en tooyour cuenta de Azure.

4. Haga clic en la suscripción de Azure > **Cuentas de almacenamiento** > su cuenta de almacenamiento > **Tablas** > **deviceData**.

   Debería ver los mensajes enviados desde el centro de IoT de tooyour dispositivos registrado en hello `deviceData` tabla.

## <a name="next-steps"></a>Pasos siguientes

Ha creado correctamente la cuenta de Azure Storage y la aplicación de función de Azure, donde se almacenan los mensajes que recibe la instancia de IoT Hub de Table Storage.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
