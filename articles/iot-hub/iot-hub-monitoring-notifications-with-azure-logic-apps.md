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
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a>Supervisión remota y notificaciones de IoT con Azure Logic Apps conectando IoT Hub y el buzón de correo

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Aplicaciones lógicas de Azure proporciona una manera de procesos de tooautomate como una serie de pasos. Una aplicación lógica puede conectar diversos servicios y protocolos. Comienza con un desencadenador como "Cuando se agregue una cuenta" y continúa con una combinación de acciones, una como "enviando una notificación de inserción". Esta característica convierte a Logic Apps en una solución de IoT perfecta para la supervisión de IoT, por ejemplo, para mantenerse alerta en busca de anomalías, entre otros escenarios de uso.

## <a name="what-you-learn"></a>Conocimientos que adquirirá

Aprenderá cómo toocreate una aplicación de la lógica que se conecta el centro de IoT y el buzón para la supervisión de temperatura y notificaciones. Cuando la temperatura de hello es superior a 30 ° C, Hola marcas de aplicación de cliente `temperatureAlert = "true"` en mensajes de bienvenida envía tooyour centro de IoT. mensaje de bienvenida de desencadenadores Hola toosend de aplicación lógica es una notificación de correo electrónico.

## <a name="what-you-do"></a>Qué debe hacer

* Crear un espacio de nombres del bus de servicio y agregue un tooit de cola.
* Agregar un punto de conexión y un centro de IoT de enrutamiento regla tooyour.
* Crear, configurar y probar una aplicación lógica.

## <a name="what-you-need"></a>Lo que necesita

* Tutorial [configurar su dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completado donde abordan las Hola según los requisitos:
  * Una suscripción de Azure activa.
  * Un centro de Azure IoT en su suscripción.
  * Una aplicación de cliente que envía el centro de IoT de Azure de tooyour de mensajes.

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a>Crear espacio de nombres de bus de servicio y agregue un tooit de cola

### <a name="create-a-service-bus-namespace"></a>Crear un espacio de nombres de Service Bus

1. En hello [portal de Azure](https://portal.azure.com/), haga clic en **New** > **integración empresarial** > **Bus de servicio**.
1. Proporcionar Hola siguiente información:

   **Nombre**: nombre de Hola Hola del bus de servicio.

   **Nivel de precios**: haga clic en **Básico** > **Seleccionar**. nivel básico de Hello es suficiente para este tutorial.

   **Grupo de recursos**: Use Hola mismo grupo de recursos que usa el centro de IoT.

   **Ubicación**: Use Hola misma ubicación que utiliza el centro de IoT.
1. Haga clic en **Crear**.

   ![Crear un espacio de nombres del bus de servicio en hello portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a>Agregar una cola de Service Bus

1. Abra el espacio de nombres del bus de servicio de hello y, a continuación, haga clic en **+ cola**.
1. Escriba un nombre para la cola de hello y, a continuación, haga clic en **crear**.
1. Abrir la cola de bus de servicio de hello y, a continuación, haga clic en **directivas de acceso compartido** > **+ agregar**.
1. Escriba un nombre para la directiva de hello, verificación **administrar**y, a continuación, haga clic en **crear**.

   ![Agregar una cola de bus de servicio en hello portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a>Agregar un punto de conexión y un centro de IoT de enrutamiento regla tooyour

### <a name="add-an-endpoint"></a>Agregación de un extremo

1. Abra IoT Hub, haga clic en Puntos de conexión > + Agregar.
1. Escriba Hola siguiente información:

   **Nombre**: nombre de Hola de punto de conexión de Hola.

   **Tipo de punto de conexión**: seleccione **Cola de Service Bus**.

   **Espacio de nombres de Bus de servicio**: seleccione Hola espacio de nombres que creó.

   **Cola de Service Bus**: cola de hello Select que ha creado.
1. Haga clic en **Aceptar**.

   ![Agregar un centro de IoT de punto de conexión tooyour Hola portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a>Agregar una regla de enrutamiento

1. En IoT Hub, haga clic en **Rutas** > **+ Agregar**.
1. Escriba Hola siguiente información:

   **Nombre**: nombre de Hola de regla de enrutamiento de Hola.

   **Origen de datos**: seleccione **DeviceMessages**.

   **Punto de conexión**: seleccionar extremo Hola que creó.

   **Cadena de consulta**: escriba `temperatureAlert = "true"`.
1. Haga clic en **Guardar**.

   ![Agregar una regla de enrutamiento de hello portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a>Crear y configurar una aplicación lógica

### <a name="create-a-logic-app"></a>Creación de una aplicación lógica

1. Hola [portal de Azure](https://portal.azure.com/), haga clic en **New** > **integración empresarial** > **aplicación lógica**.
1. Escriba Hola siguiente información:

   **Nombre**: nombre de Hola de aplicación lógica de hello.

   **Grupo de recursos**: Use Hola mismo grupo de recursos que usa el centro de IoT.

   **Ubicación**: Use Hola misma ubicación que utiliza el centro de IoT.
1. Haga clic en **Crear**.

### <a name="configure-hello-logic-app"></a>Configurar la aplicación de la lógica de hello

1. Abra la aplicación de lógica de Hola que se abre en hello lógica el Diseñador de aplicaciones.
1. Hola lógica el Diseñador de aplicaciones, haga clic en **en blanco de lógica de aplicación**.

   ![Comenzar con una aplicación lógica en blanco en hello portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. Haga clic en **Service Bus**.

   ![Seleccione toostart de Service Bus crear la aplicación lógica en hello portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. Haga clic en **Service Bus: Cuando llegan uno o más mensajes a una cola (autocompletar)**.
1. Cree una conexión de Service Bus.
   1. Escriba un nombre de conexión.
   1. Haga clic en el espacio de nombres del bus de servicio de hello > Hola directiva de bus de servicio > **crear**.

      ![Crear una conexión de bus de servicio para la aplicación lógica en hello portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. Haga clic en **continuar** después de crean conexiones de bus de servicio de Hola.
   1. Seleccione cola Hola que creó y escriba `175` para **recuento máximo de mensaje**

      ![Especifique el número de máximo de los mensajes de Hola para conexiones de bus de servicio de hello en la aplicación lógica](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. Haga clic en "Guardar" botón toosave Hola cambios.

1. Cree una conexión de servicio SMTP.
   1. Haga clic en **Nuevo paso** > **Agregar una acción**.
   1. Tipo de `SMTP`, haga clic en hello **SMTP** de servicio en el resultado de la búsqueda de hello y, a continuación, haga clic en **SMTP - enviar correo electrónico**.

      ![Crear una conexión de SMTP en la aplicación lógica en hello portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. Escriba información de hello SMTP del buzón de correo y, a continuación, haga clic en **crear**.

      ![Escriba la información de conexión de SMTP en la aplicación lógica en hello portal de Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      Obtener información de hello SMTP de [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), y [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).
   1. Escriba la dirección de correo electrónico en **De** y **Para** y `High temperature detected` en **Asunto** y **Cuerpo**.
   1. Haga clic en **Guardar**.

aplicación de la lógica de Hello está en condiciones de funcionamiento cuando la guarde.

## <a name="test-hello-logic-app"></a>Aplicación de prueba hello lógica

1. Iniciar aplicación de cliente de Hola que implemente dispositivo tooyour en [ESP8266 conectar tooAzure centro de IoT](iot-hub-arduino-huzzah-esp8266-get-started.md).
1. Aumentar la temperatura del entorno de hello alrededor de hello SensorTag toobe superior a 30 C. Por ejemplo, claro una vela alrededor de su SensorTag.
1. Debería recibir una notificación por correo electrónico enviada por la aplicación de la lógica de hello.

   > [!NOTE]
   > El proveedor de servicios de correo electrónico que necesite tooverify Hola remitente identidad toomake seguro es quién envía correo electrónico de Hola.

## <a name="next-steps"></a>Pasos siguientes

Ha creado correctamente una aplicación lógica que conecta IoT Hub y el buzón de correo para la supervisión de temperatura y las notificaciones.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
