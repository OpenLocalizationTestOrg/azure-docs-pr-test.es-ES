---
title: los extremos del centro de IoT de Azure aaaUnderstand | Documentos de Microsoft
description: "Guía para desarrolladores: información de referencia sobre los puntos de conexión orientados a dispositivos y servicios IoT Hub."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 57ba52ae-19c6-43e4-bc6c-d8a5c2476e95
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 8647f15d2f2a050ad5799ea82f4d2d46db0dbec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-endpoints"></a>Referencia: Puntos de conexión de IoT Hub

## <a name="iot-hub-names"></a>Nombres de IoT Hub

Puede encontrar Hola nombre del centro de IoT de Hola que hospeda los extremos en el portal de hello en hello **Introducción** hoja. De forma predeterminada, el nombre DNS de Hola de un centro de IoT es similar: `{your iot hub name}.azure-devices.net`.

Puede utilizar DNS de Azure toocreate un nombre DNS personalizado para su centro de IoT. Para obtener más información, consulte [configuración de dominio personalizado de tooprovide de DNS de Azure de uso para un servicio de Azure](../dns/dns-custom-domain.md#azure-iot).

## <a name="list-of-built-in-iot-hub-endpoints"></a>Lista de puntos de conexión de IoT Hub integrados

Centro de IoT de Azure es un servicio multiempresa que expone sus actores toovarious de funcionalidad. Hello siguiente diagrama muestra hello varios extremos que expone el centro de IoT.

![Puntos de conexión de IoT Hub][img-endpoints]

Hola lista siguiente describe los puntos de conexión de hello:

* **Proveedor de recursos**. expone Hello proveedor de recursos de centro de IoT un [Azure Resource Manager] [ lnk-arm] interfaz. Esta interfaz permite toocreate de propietarios de suscripción de Azure y eliminar centros de IoT y propiedades de centro de IoT tooupdate. Propiedades de centro de IoT rigen [las directivas de seguridad de nivel de concentrador][lnk-accesscontrol], en lugar de control de acceso de nivel de toodevice y opciones funcionales para la mensajería en la nube al dispositivo y el dispositivo a la nube. Hello proveedor de recursos de centro de IoT también le permite demasiado[Exportar identidades de dispositivos][lnk-importexport].
* **Administración de identidades de dispositivo**. Cada centro de IoT expone un conjunto de identidades de dispositivos de toomanage de puntos de conexión de REST de HTTP (crear, recuperar, actualizar y eliminar). Las [identidades del dispositivo][lnk-device-identities] se usan para autenticación de dispositivos y control de acceso.
* **Administración de dispositivo gemelo**. Cada centro de IoT expone un conjunto de tooquery de punto de conexión de REST de HTTP y la actualización de servicio orientado [: los gemelos de dispositivo] [ lnk-twins] (actualización de etiquetas y propiedades).
* **Administración de trabajos**. Cada centro de IoT expone un conjunto de tooquery de punto de conexión de REST de HTTP a nivel de servicio y administrar [trabajos][lnk-jobs].
* **Puntos de conexión de dispositivo**. Para cada dispositivo en el registro de la identidad de hello, centro de IoT expone un conjunto de puntos de conexión:

  * *Envío de mensajes de dispositivo a nube*. Un dispositivo utiliza este extremo demasiado[enviar mensajes del dispositivo a la nube][lnk-d2c].
  * *Recepción de mensajes de nube a dispositivo*. Un dispositivo usa este tooreceive de punto de conexión de destino [mensajes en la nube al dispositivo][lnk-c2d].
  * *Iniciar cargas de archivos*. Un dispositivo usa este tooreceive de punto de conexión un URI de SAS de almacenamiento de Azure desde el centro de IoT demasiado[cargar un archivo][lnk-upload].
  * *Recuperación y actualización de las propiedades del dispositivo gemelo*. Un dispositivo usa este extremo tooaccess su [gemelas dispositivo][lnk-twins]de propiedades.
  * *Recepción de solicitudes de métodos directos*. Un dispositivo usa este toolisten de punto de conexión para [método directo][lnk-methods]de solicitudes.

    Estos puntos de conexión se exponen mediante los protocolos[ MQTT v3.1.1][lnk-mqtt], HTTP 1.1 y [AMQP 1.0][lnk-amqp]. AMQP también está disponible sobre [WebSockets][lnk-websockets] en el puerto 443.

    Hello puntos de conexión de dispositivo: los gemelos y métodos están disponibles solo cuando se usa hello [MQTT v3.1.1] [ lnk-mqtt] protocolo.

* **Puntos de conexión de servicio**. Cada centro de IoT expone un conjunto de puntos de conexión para su toocommunicate de back-end de la solución con los dispositivos. Con una excepción, estos puntos de conexión sólo se muestran con hello [AMQP] [ lnk-amqp] protocolo. extremo de invocación de método de Hola se expone en hello protocolo HTTP.
  
  * *Recepción de mensajes de dispositivo a nube*. Este punto de conexión es compatible con [Azure Event Hubs][lnk-event-hubs]. Un servicio back-end puede usarlo hello tooread [mensajes del dispositivo a la nube] [ lnk-d2c] enviados por los dispositivos. Puede crear extremos personalizados en su centro de IoT en punto de conexión de adición toothis integrados.
  * *Envío de mensajes de nube a dispositivo y recepción de confirmaciones de entrega*. Estos extremos permiten su toosend de back-end de la solución confiable [mensajes en la nube al dispositivo][lnk-c2d], y tooreceive Hola confirmaciones de entrega o expiración correspondientes.
  * *Recepción de notificaciones de archivos*. Este extremo de mensajería permite tooreceive notificaciones de cuando los dispositivos cargar correctamente un archivo. 
  * *Invocación del método director*. Este punto de conexión permite a un servicio back-end tooinvoke una [método directo] [ lnk-methods] en un dispositivo.
  * *Recepción de eventos de supervisión de operaciones*. Este punto de conexión permite operaciones de tooreceive eventos de supervisión si el IoT hub ha sido configurado tooemit ellos. Para más información, consulte [Supervisión de operaciones de IoT Hub][lnk-operations-mon].

Hola [SDK de Azure IoT] [ lnk-sdks] artículo describe Hola tooaccess de varias maneras de estos puntos de conexión.

Todos los extremos de centro de IoT usan hello [TLS] [ lnk-tls] protocolo y ningún extremo nunca se expone en los canales sin cifrar/no segura.

## <a name="custom-endpoints"></a>Puntos de conexión personalizados

Puede vincular los servicios de Azure existentes en su tooact de centro de IoT de suscripción tooyour como puntos de conexión para el enrutamiento de mensajes. Estos puntos de conexión hacen de puntos de conexión de servicio y se usan como receptores para las rutas de los mensajes. Dispositivos no pueden escribir directamente toohello extremos adicionales. toolearn más información acerca de las rutas de mensajes, vea la entrada de guía para desarrolladores de hello en [enviar y recibir mensajes con el centro de IoT][lnk-devguide-messaging].

Centro de IoT admite actualmente Hola después de los servicios de Azure como extremos adicionales:

* Centros de eventos
* Colas de Service Bus
* Temas de Service Bus

Centro de IoT necesita extremos de servicio de acceso de escritura toothese para toowork de enrutamiento de mensajes. Si configura los extremos a través de hello portal de Azure, se agregan los permisos necesarios de Hola. Asegúrese de que configurar el rendimiento de servicios toosupport Hola esperado. Al configurar la solución de IoT en primer lugar, puede necesita toomonitor los extremos adicionales y realizar los ajustes necesarios para la carga real Hola.

Si un mensaje coincide con varias rutas que señalan todos toohello mismo extremo, centro de IoT ofrece el punto de conexión de mensajes toothat una sola vez. Por lo tanto, es necesario desduplicación del tooconfigure en la cola de Bus de servicio o un tema. En las colas con particiones, la afinidad de partición garantiza el orden de los mensajes.

> [!NOTE]
> Las colas y los temas de Service Bus usados como puntos de conexión de IoT Hub no deben tener habilitadas las opciones **Sesiones** o **Detección de duplicados**. Si cualquiera de estas opciones están habilitada, el punto de conexión de hello aparece como **inaccesible** Hola portal de Azure.

Para los límites de hello en número de Hola de puntos de conexión que se puede agregar, consulte [cuotas y limitación][lnk-devguide-quotas].

## <a name="field-gateways"></a>Puertas de enlace de campo

En una solución de IoT, un *puerta de enlace de campo* se encuentra entre los dispositivos y los puntos de conexión de IoT Hub. Es suele encontrarse tooyour cerrar dispositivos. Los dispositivos se comunican directamente con la puerta de enlace de campo de hello mediante un protocolo compatible con dispositivos de Hola. puerta de enlace de campo de Hello conecta tooan extremo del centro de IoT mediante un protocolo que es compatible con el centro de IoT. Una puerta de enlace de campo puede ser un dispositivo de hardware dedicado o un equipo de bajo consumo de energía que ejecuta el software de puerta de enlace personalizado.

Puede usar [Azure IoT borde] [ lnk-iot-edge] tooimplement una puerta de enlace de campo. Borde de IoT ofrece una funcionalidad como multiplexación comunicaciones desde varios dispositivos en hello misma conexión de centro de IoT.

## <a name="next-steps"></a>Pasos siguientes

Otros temas de referencia en la Guía del desarrollador de IoT Hub son:

* [Referencia: Lenguaje de consulta de IoT Hub para dispositivos gemelos y trabajos][lnk-devguide-query]
* [Cuotas y limitación][lnk-devguide-quotas]
* [Compatibilidad con MQTT de IoT Hub][lnk-devguide-mqtt]

[lnk-iot-edge]: https://github.com/Azure/iot-edge

[img-endpoints]: ./media/iot-hub-devguide-endpoints/endpoints.png
[lnk-amqp]: https://www.amqp.org/
[lnk-mqtt]: http://mqtt.org/
[lnk-websockets]: https://tools.ietf.org/html/rfc6455
[lnk-arm]: ../azure-resource-manager/resource-group-overview.md
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/

[lnk-tls]: https://tools.ietf.org/html/rfc5246


[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-accesscontrol]: iot-hub-devguide-security.md#access-control-and-permissions
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-device-identities]: iot-hub-devguide-identity-registry.md
[lnk-upload]: iot-hub-devguide-file-upload.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md

[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[lnk-operations-mon]: iot-hub-operations-monitoring.md
