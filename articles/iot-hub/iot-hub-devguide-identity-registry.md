---
title: registro de identidad de aaaUnderstand Hola centro de IoT de Azure | Documentos de Microsoft
description: "Guía del desarrollador - descripción de hello del registro de identidad de centro de IoT y cómo toouse se toomanage los dispositivos. Incluye información sobre Hola importación y exportación de identidades de dispositivos de forma masiva."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0706eccd-e84c-4ae7-bbd4-2b1a22241147
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c9fe3730a4608e28c47807ecb42e13e73f6a2e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-identity-registry-in-your-iot-hub"></a>Comprender el registro de la identidad de hello en el centro de IoT

Cada centro de IoT tiene un registro de la identidad que almacena información acerca de los dispositivos de hello permiten tooconnect toohello IoT hub. Antes de que un dispositivo puede conectarse tooan centro de IoT, debe haber una entrada para ese dispositivo en el registro de identidad del centro de IoT Hola. Un dispositivo también debe autenticarse con el centro de IoT de hello en función de las credenciales almacenadas en el registro de la identidad de Hola.

Id. de dispositivo de Hello almacenado en el registro de la identidad de hello distingue mayúsculas de minúsculas.

En un nivel alto, del registro de la identidad de hello es una colección compatibles con el resto de recursos de la identidad de dispositivo. Cuando se agrega una entrada en el registro de la identidad de hello, centro de IoT crea un conjunto de recursos por dispositivo como una cola de Hola que contiene mensajes de nube al dispositivo en curso.

### <a name="when-toouse"></a>Cuando toouse

Utilizar el registro de la identidad de hello cuando necesite:

* Aprovisione los dispositivos que se conectan tooyour centro de IoT.
* Controlar los puntos de conexión de dispositivo del concentrador de tooyour de acceso por dispositivo.

> [!NOTE]
> registro de la identidad de Hello no contiene los metadatos específicos de la aplicación.

## <a name="identity-registry-operations"></a>Operaciones de registro de identidad

Hola del registro de identidad de centro de IoT expone hello las siguientes operaciones:

* Crear la identidad del dispositivo
* Actualizar la identidad del dispositivo
* Recuperar la identidad del dispositivo mediante el identificador
* Eliminar la identidad del dispositivo
* Lista de identidades de too1000
* Exportar todo el almacenamiento de identidades tooAzure blob
* Importar todas las identidades desde Azure Blob Storage

Todas estas operaciones pueden usar la simultaneidad optimista, tal como se especifica en [RFC7232][lnk-rfc7232].

> [!IMPORTANT]
> Hola solo forma tooretrieve todas las identidades de registro de la identidad de un centro de IoT es hello de toouse [exportar] [ lnk-export] funcionalidad.

Un registro de identidades de un centro de IoT:

* No contiene los metadatos de la aplicación.
* Puede obtenerse acceso como un diccionario, mediante el uso de hello **deviceId** como clave de Hola.
* No admite consultas expresivas.

Una solución de IoT normalmente tiene un almacén independiente específico de la solución que contiene los metadatos específicos de la aplicación. Por ejemplo, hello almacén específica de la solución en una solución de creación inteligente registraría sala de hello en el que se implementa un sensor de temperatura.

> [!IMPORTANT]
> Usar solo del registro de identidad de Hola para operaciones de aprovisionamiento y administración de dispositivos. Las operaciones de alto rendimiento en tiempo de ejecución no deben depender realizar operaciones en el registro de la identidad de Hola. Por ejemplo, la comprobación de estado de conexión de Hola de un dispositivo antes de enviar un comando no es un patrón admitido. Realizar seguro hello toocheck [limitación tasas] [ lnk-quotas] de registro de la identidad de Hola y Hola [latido de dispositivo] [ lnk-guidance-heartbeat] patrón.

## <a name="disable-devices"></a>Deshabilitar dispositivos

Puede deshabilitar dispositivos mediante la actualización de hello **estado** propiedad de una identidad en el registro de la identidad de Hola. Normalmente, esta propiedad se usa en dos escenarios:

* Durante el proceso de orquestación de aprovisionamiento. Para más información, consulte [Aprovisionamiento de dispositivos][lnk-guidance-provisioning].
* Si por cualquier motivo considera que un dispositivo está en peligro o no está autorizado.

## <a name="import-and-export-device-identities"></a>Importar y exportar identidades de dispositivo

Puede exportar identidades de dispositivos de forma masiva desde el registro de identidad de un centro de IoT, mediante el uso de las operaciones asincrónicas en hello [punto de conexión del proveedor de recursos de centro de IoT][lnk-endpoints]. Las exportaciones se larga ejecución trabajos que usan una datos de identidad de dispositivo de blob proporcionado por el cliente contenedor toosave leen desde el registro de la identidad de Hola.

Puede importar las identidades del dispositivo en el registro de identidad del centro de IoT de forma masiva tooan, mediante las operaciones asincrónicas en hello [punto de conexión del proveedor de recursos de centro de IoT][lnk-endpoints]. Las importaciones son los trabajos de larga ejecución que usan datos de una blob proporcionado por el cliente contenedor toowrite dispositivo identidad de datos en el registro de la identidad de Hola.

* Para obtener información detallada acerca de hello importar y exportar las API, consulte [API de REST de proveedor de recursos de centro de IoT][lnk-resource-provider-apis].
* toolearn más acerca de cómo ejecutar importarán y exportación los trabajos, consulte [administración de identidades de dispositivos del centro de IoT de forma masiva][lnk-bulk-identity].

## <a name="device-provisioning"></a>Aprovisionamiento de dispositivos

datos del dispositivo Hola que almacena una solución de IoT dada dependen de los requisitos específicos de saludo de la solución. Sin embargo, como mínimo, una solución debe almacenar identidades del dispositivo y claves de autenticación. El IoT Hub incluye un registro de identidades que puede almacenar valores para cada dispositivo como identificadores, claves de autenticación y códigos de estado. Una solución puede utilizar otros servicios de Azure como almacenamiento de tabla, almacenamiento de blobs o Cosmos DB toostore ningún dato de dispositivo adicionales.

*Aprovisionamiento de dispositivos* es Hola proceso de agregar datos toohello almacenes de hello inicial del dispositivo en la solución. tooenable un nuevo centro de tooyour tooconnect de dispositivo, debe agregar un dispositivo Id. y claves toohello del registro de identidad de centro de IoT. Como parte del proceso de aprovisionamiento de hello, podría necesitar datos específicos del dispositivo de tooinitialize en otros almacenes de solución.

## <a name="device-heartbeat"></a>Latido de dispositivo

registro de la identidad de centro de IoT Hello contiene un campo denominado **connectionState**. Usar solo hello **connectionState** campo durante el desarrollo y depuración. Soluciones de IoT no deben consultar el campo de hello en tiempo de ejecución. Por ejemplo, ¿consultan hello **connectionState** toocheck de campo si está conectado un dispositivo antes de enviar un mensaje en la nube al dispositivo o un SMS.

Si la solución de IoT necesita tooknow si está conectado un dispositivo, debe implementar hello *patrón latido*.

En el patrón de latido de hello, dispositivo Hola envía mensajes del dispositivo a la nube al menos una vez cada cantidad fija de tiempo (por ejemplo, al menos una vez cada hora). Por lo tanto, incluso si un dispositivo no tiene ningún toosend de datos, envía un mensaje de dispositivo para la nube vacío (normalmente con una propiedad que lo identifica como un latido) todavía. En el lado del servicio hello, solución de hello mantiene un mapa con el último latido de hello recibido para cada dispositivo. Si la solución de hello no recibe un mensaje de latido en tiempo de espera de Hola desde dispositivo hello, se supone que hay un problema con el dispositivo de Hola.

Una implementación más compleja puede incluir información de Hola de [supervisión de operaciones] [ lnk-devguide-opmon] tooidentify dispositivos que están tratando de tooconnect o comunicaran, pero un error. Al implementar el patrón de latido de hello, asegúrese de seguro toocheck [IoT Hub cuotas y aceleradores][lnk-quotas].

> [!NOTE]
> Si una conexión de hello IoT solución usa estado toodetermine solamente si toosend los mensajes en la nube al dispositivo, y los mensajes son no difusión toolarge conjuntos de dispositivos, considere el uso más simple de hello *breve de la hora de expiración* patrón. Este patrón logra Hola el mismo resultado como mantener un registro de estado de conexión de dispositivo mediante el patrón de latido de hello, al ser más eficiente. Si se solicitan los reconocimientos de mensajes, centro de IoT puede notificarle acerca de qué dispositivos están tooreceive capaz de mensajes y cuáles no.

## <a name="device-lifecycle-notifications"></a>Notificaciones de ciclo de vida de dispositivo

IoT Hub puede notificar la solución de IoT al crearse o eliminarse la identidad de un dispositivo mediante el envío de notificaciones de ciclo de vida de dispositivo. toodo por lo tanto, la solución de IoT necesita toocreate una ruta e igual de origen de datos de hello tooset demasiado*DeviceLifecycleEvents*. De forma predeterminada, no se envían notificaciones de ciclo de vida, es decir, no existen previamente tales rutas. mensaje de notificación de Hello incluye propiedades y cuerpo.

Propiedades: Propiedades de sistema de mensajes tienen el prefijo hello `'$'` símbolos.

| Nombre | Valor |
| --- | --- |
$content-type | application/json |
$iothub-enqueuedtime |  Hora de envían de notificaciones de Hola |
$iothub-message-source | deviceLifecycleEvents |
$content-encoding | utf-8 |
opType | **createDeviceIdentity** o **deleteDeviceIdentity** |
hubName | Nombre de IoT Hub |
deviceId | Id. de dispositivo de Hola |
operationTimestamp | Marca de tiempo ISO8601 de operación |
iothub-message-schema | deviceLifecycleNotification |

Cuerpo: Esta sección está en formato JSON y representa a gemelas Hola de hello creado la identidad del dispositivo. Por ejemplo,

```json
{
    "deviceId":"11576-ailn-test-0-67333793211",
    "etag":"AAAAAAAAAAE=",
    "properties": {
        "desired": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        },
        "reported": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        }
    }
}
```

## <a name="reference-topics"></a>Temas de referencia:

Hello temas de referencia siguientes proporcionan más información acerca del registro de identidad de Hola.

## <a name="device-identity-properties"></a>Propiedades de identidad del dispositivo

Identidades de dispositivos se representan como documentos JSON con hello propiedades siguientes:

| Propiedad | Opciones | Description |
| --- | --- | --- |
| deviceId |necesarias, de solo lectura en actualizaciones |Una cadena entre mayúsculas y minúsculas (arriba too128 caracteres) de caracteres alfanuméricos ASCII 7 bits + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`. |
| generationId |requerido, de solo lectura |Una IoT entre mayúsculas y minúsculas, generado por el centro de cadena de too128 caracteres. Este valor es toodistinguish usa dispositivos con hello mismo **deviceId**, cuando se elimina y vuelve a crear. |
| ETag |requerido, de solo lectura |Una cadena que representa una etiqueta ETag no segura para la identidad del dispositivo hello, como por [RFC7232][lnk-rfc7232]. |
| auth |opcional |Un objeto compuesto que contiene material de seguridad e información de autenticación. |
| auth.symkey |opcional |Un objeto compuesto que contiene una clave principal y una secundaria, almacenadas en formato base64. |
| status |requerido |Indicador de acceso Puede ser **Habilitado** o **Deshabilitado**. Si **habilitado**, Hola puede tooconnect. Si está **Dishabilitado**, este dispositivo no puede obtener acceso a ningún punto de conexión accesible desde el dispositivo. |
| statusReason |opcional |Un 128 caracteres de longitud de cadena esa razón de hello almacenes Hola estado de dispositivo identidad. Se permiten todos los caracteres UTF-8. |
| statusUpdateTime |solo lectura |Un indicador temporal, que muestra hello fecha y hora de la última actualización de estado Hola. |
| connectionState |solo lectura |Un campo que indica el estado de la conexión: **Conectado** o **Desconectado**. Este campo representa Hola vista de centro de IoT del estado de conexión de dispositivo de Hola. **Importante**: Este campo debe usarse solo para fines de desarrollo o depuración. estado de conexión de Hola se actualiza solo para dispositivos con MQTT o AMQP. Además, se basa en pings de nivel de protocolo (pings MQTT o pings AMQP) y puede tener un retraso de 5 minutos como máximo. Por estos motivos es posible que haya falsos positivos, como dispositivos que se notifican como conectados pero que están desconectados. |
| connectionStateUpdatedTime |solo lectura |Se actualizó un indicador temporal, que muestra la fecha de Hola y estado de conexión de Hola de última hora. |
| lastActivityTime |solo lectura |Un indicador temporal, que muestra la fecha de Hola y último dispositivo de hello tiempo conectado, que recibe o envía un mensaje. |

> [!NOTE]
> Estado de conexión sólo puede representar Hola vista de centro de IoT del estado de Hola de conexión de Hola. Estado de las actualizaciones toothis se puede retrasar según las configuraciones y las condiciones de red.

## <a name="additional-reference-material"></a>Material de referencia adicional

Otros temas de referencia en la Guía del desarrollador de centro de IoT Hola incluyen:

* [Los extremos del centro de IoT] [ lnk-endpoints] describe Hola varios extremos que cada centro de IoT expone las operaciones de tiempo de ejecución y administración.
* [Limitación y las cuotas] [ lnk-quotas] describe las cuotas de Hola y comportamientos que se aplican toohello servicio del centro de IoT de limitación.
* [SDK de dispositivos y servicios de Azure IoT] [ lnk-sdks] listas Hola lenguaje varios SDK que se puede usar cuando se desarrollan aplicaciones de dispositivos y servicios que interactúan con el centro de IoT.
* [Lenguaje de consulta de centro de IoT] [ lnk-query] describe el lenguaje de consulta de Hola que puede utilizar información tooretrieve centro de IoT de: los gemelos de dispositivo y trabajos.
* [Compatibilidad de IoT Hub MQTT] [ lnk-devguide-mqtt] proporciona más información acerca del soporte técnico de centro de IoT para el protocolo MQTT Hola.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido cómo del registro de identidad de centro de IoT de toouse hello, puede que esté interesado en hello temas de guía para desarrolladores de centro de IoT siguientes:

* [Controlar el acceso tooIoT concentrador][lnk-devguide-security]
* [Usar el estado del dispositivo: los gemelos toosynchronize y configuraciones][lnk-devguide-device-twins]
* [Invocación de un método directo en un dispositivo][lnk-devguide-directmethods]
* [Programación de trabajos en varios dispositivos][lnk-devguide-jobs]

Si desea que tootry algunos de los conceptos de hello descritos en este artículo, es posible que interesa Hola sigue tutorial del centro de IoT:

* [Introducción a Azure IoT Hub][lnk-getstarted-tutorial]

<!-- Links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-guidance-provisioning]: iot-hub-devguide-identity-registry.md#device-provisioning
[lnk-guidance-heartbeat]: iot-hub-devguide-identity-registry.md#device-heartbeat
[lnk-rfc7232]: https://tools.ietf.org/html/rfc7232
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-export]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-devguide-opmon]: iot-hub-operations-monitoring.md

[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
