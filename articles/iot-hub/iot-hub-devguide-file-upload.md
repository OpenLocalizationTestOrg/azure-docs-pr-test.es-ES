---
title: cargar el archivo aaaUnderstand centro de IoT de Azure | Documentos de Microsoft
description: "Guía del desarrollador - característica de carga de archivo uso Hola de toomanage centro de IoT cargar archivos desde un contenedor de blobs de dispositivo tooan almacenamiento de Azure."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a0427925-3e40-4fcd-96c1-2a31d1ddc14b
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: d44f9303ead4fa282dc0baf70887af1b8a03293d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-with-iot-hub"></a>Carga de archivos con IoT Hub

Tal como se detalla en hello [los extremos del centro de IoT] [ lnk-endpoints] artículo, un dispositivo puede iniciar una carga de archivo mediante el envío de una notificación a través de un punto de conexión de dispositivo (**/devices/ {deviceId} / archivos**). Cuando un dispositivo notifica al centro de IoT que una carga completa, centro de IoT envía un mensaje de notificación de la carga de archivos a través de hello **/messages/servicebound/filenotifications** a nivel de servicio de punto de conexión.

En lugar de mensajes a través del centro de IoT propio de intermediación, centro de IoT en su lugar, actúa como un tooan distribuidor había asociado de cuenta de almacenamiento de Azure. Un dispositivo solicita un token de almacenamiento del centro de IoT es específico toohello archivo hello dispositivo desea tooupload. dispositivo de Hello usa Hola URI de SAS tooupload Hola archivo toostorage y, cuando se completa la carga de hello dispositivo Hola envía una notificación de finalización tooIoT concentrador. Centro de IoT comprueba la carga de archivos de hello es completa y, a continuación, agrega un extremo de notificación archivo carga notificación mensaje toohello a nivel de servicio archivo.

Antes de cargar un archivo tooIoT concentrador desde un dispositivo, debe configurar el centro por [asociar un almacenamiento de Azure] [ lnk-associate-storage] tooit de la cuenta.

El dispositivo puede, a continuación, [inicializar una carga] [ lnk-initialize] y, a continuación, [notificar al centro de IoT] [ lnk-notify] cuando finalice la carga de Hola. Si lo desea, cuando un dispositivo notifica al centro de IoT esa carga de hello finalización, el servicio Hola puede generar un [mensaje de notificación][lnk-service-notification].

### <a name="when-toouse"></a>Cuando toouse

Usar archivos de medios de toosend de carga de archivos y los lotes de telemetría grandes cargados por dispositivos conectados de forma intermitente o ancho de banda de toosave comprimido.

Consulte demasiado[Guía de comunicación de dispositivos a la nube] [ lnk-d2c-guidance] si está en duda entre usar propiedades notificados, mensajes del dispositivo a la nube o cargar el archivo.

## <a name="associate-an-azure-storage-account-with-iot-hub"></a>Asociar una cuenta de Azure Storage con IoT Hub

funcionalidad de carga de archivos de hello toouse, primero debe vincular un toohello de cuenta de almacenamiento de Azure centro de IoT. Puede completar esta tarea a través de hello [portal de Azure][lnk-management-portal], o mediante programación a través de hello [API de REST de proveedor de recursos de centro de IoT] [ lnk-resource-provider-apis]. Una vez que haya asociado una cuenta de almacenamiento de Azure con el centro de IoT, Hola servicio devuelve un URI de SAS tooa dispositivo al dispositivo de hello inicia una solicitud de carga de archivo.

> [!NOTE]
> Hola [SDK de Azure IoT] [ lnk-sdks] automáticamente Hola a recuperar el identificador URI de SAS, cargar archivo hello y notificar el centro de IoT de una carga completada.


## <a name="initialize-a-file-upload"></a>Inicialización de una carga de archivos
Centro de IoT tiene un extremo concreto para dispositivos toorequest un URI de SAS para tooupload un archivo de almacenamiento. proceso de carga de archivos de hello tooinitiate, Hola dispositivo envía una solicitud POST demasiado`{iot hub}.azure-devices.net/devices/{deviceId}/files` con hello siguiendo el cuerpo JSON:

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

Centro de IoT devuelve Hola datos, qué dispositivo hello usa el archivo de hello tooupload siguientes:

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a>En desuso: inicializar una carga de archivo con un comando GET

> [!NOTE]
> Esta sección describe la funcionalidad en desuso para saber cómo tooreceive un URI de SAS del centro de IoT. Utilice el método POST de Hola que se ha descrito anteriormente.

Centro de IoT tiene dos archivos de toosupport de extremos REST cargar uno tooget Hola URI de SAS para el almacenamiento y Hola otro centro de IoT de hello toonotify de una carga completada. Hello dispositivo inicia el proceso de carga de archivos de hello mediante el envío de un centro de IoT GET toohello en `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`. Centro de IoT Hola devuelve:

* Un URI de SAS toohello específico archivo toobe cargado.
* Un identificador de correlación toobe usa una vez completada la carga de Hola.

## <a name="notify-iot-hub-of-a-completed-file-upload"></a>Notificación a IoT Hub de una carga de archivos completada

dispositivo de Hello es responsable de cargar Hola archivo toostorage mediante SDK de almacenamiento de Azure Hola. Una vez completada la carga de hello, dispositivo Hola envía una solicitud POST demasiado`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` con hello siguiendo el cuerpo JSON:

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

Hola valo `isSuccess` es un valor Boolean que indica si el archivo hello se cargó correctamente. Hola código de estado de `statusCode` es Hola estado para la carga de Hola de toostorage de archivo de Hola y Hola `statusDescription` corresponde toohello `statusCode`.

## <a name="reference-topics"></a>Temas de referencia:

Hello temas de referencia siguientes proporcionan más información sobre cómo descargar archivos desde un dispositivo.

## <a name="file-upload-notifications"></a>Notificaciones de carga de archivos

Si lo desea, cuando un dispositivo notifica al centro de IoT que una carga completa, centro de IoT puede generar un mensaje de notificación que contiene Hola nombre y ubicación de almacenamiento de archivo hello.

Como se ha explicado en [Puntos de conexión][lnk-endpoints], IoT Hub entrega notificaciones de carga de archivos a través de un punto de conexión accesible desde el servicio (**/messages/servicebound/fileuploadnotifications**) en forma de mensajes. Hola semántica de recepción de notificaciones de carga de archivos son Hola igual que para los mensajes en la nube al dispositivo y ha Hola mismo [message Lifecycle-español][lnk-lifecycle]. Cada mensaje recuperado de extremo de notificación de carga de archivo hello es un registro JSON con hello propiedades siguientes:

| Propiedad | Description |
| --- | --- |
| EnqueuedTimeUtc |Marca de tiempo que indica cuando se creó la notificación de Hola. |
| deviceId |**Id. de dispositivo** de dispositivo de Hola que cargan el archivo hello. |
| BlobUri |URI del archivo hello cargado. |
| BlobName |Nombre del programa Hola a carga el archivo. |
| LastUpdatedTime |Marca de tiempo que indica cuándo se actualizó por última vez archivo hello. |
| BlobSizeInBytes |Tamaño del programa Hola a carga el archivo. |

**Ejemplo**. Este ejemplo se muestra el cuerpo Hola de un archivo de carga de mensaje de notificación.

```json
{
    "deviceId":"mydevice",
    "blobUri":"https://{storage account}.blob.core.windows.net/{container name}/mydevice/myfile.jpg",
    "blobName":"mydevice/myfile.jpg",
    "lastUpdatedTime":"2016-06-01T21:22:41+00:00",
    "blobSizeInBytes":1234,
    "enqueuedTimeUtc":"2016-06-01T21:22:43.7996883Z"
}
```

## <a name="file-upload-notification-configuration-options"></a>Opciones de configuración de notificaciones de carga de archivos

Cada centro de IoT expone Hola siguientes opciones de configuración para las notificaciones de carga de archivo:

| Propiedad | Description | Intervalo y valor predeterminado |
| --- | --- | --- |
| **enableFileUploadNotifications** |Controla si las notificaciones de carga de archivo se escriben toohello extremo de notificaciones de archivo. |Bool. Valor predeterminado: True. |
| **fileNotifications.ttlAsIso8601** |TTL predeterminado para las notificaciones de carga de archivos. |Intervalo de ISO_8601 una too48H (1 minuto como mínimo). Valor predeterminado: 1 hora. |
| **fileNotifications.lockDuration** |Duración del bloqueo de la cola de notificaciones de carga de archivos de Hola. |5 too300 segundos (5 segundos como mínimos). Valor predeterminado: 60 segundos. |
| **fileNotifications.maxDeliveryCount** |Número máximo de entregas de archivo hello cargar cola de notificación. |1 too100. Valor predeterminado: 100. |

## <a name="additional-reference-material"></a>Material de referencia adicional

Otros temas de referencia en la Guía del desarrollador de centro de IoT Hola incluyen:

* [Los extremos del centro de IoT] [ lnk-endpoints] describe Hola varios extremos que cada centro de IoT expone las operaciones de tiempo de ejecución y administración.
* [Limitación y las cuotas] [ lnk-quotas] describe las cuotas de Hola y comportamientos que se aplican toohello servicio del centro de IoT de limitación.
* [SDK de dispositivos y servicios de Azure IoT] [ lnk-sdks] listas Hola lenguaje varios SDK que se puede usar cuando se desarrollan aplicaciones de dispositivos y servicios que interactúan con el centro de IoT.
* [Lenguaje de consulta de centro de IoT] [ lnk-query] describe el lenguaje de consulta de Hola que puede utilizar información tooretrieve centro de IoT de: los gemelos de dispositivo y trabajos.
* [Compatibilidad de IoT Hub MQTT] [ lnk-devguide-mqtt] proporciona más información acerca del soporte técnico de centro de IoT para el protocolo MQTT Hola.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido cómo tooupload los archivos de dispositivos mediante el centro de IoT, es posible que interesa Hola temas de guía para desarrolladores de centro de IoT siguientes:

* [Administrar identidades del dispositivo en IoT Hub][lnk-devguide-identities]
* [Controlar el acceso tooIoT concentrador][lnk-devguide-security]
* [Usar el estado del dispositivo: los gemelos toosynchronize y configuraciones][lnk-devguide-device-twins]
* [Invocación de un método directo en un dispositivo][lnk-devguide-directmethods]
* [Programación de trabajos en varios dispositivos][lnk-devguide-jobs]

Si desea que tootry algunos de los conceptos de hello descritos en este artículo, es posible que interesa Hola sigue tutorial del centro de IoT:

* [Funcionamiento de cloud archivos tooupload de toohello de dispositivos con el centro de IoT][lnk-fileupload-tutorial]

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-management-portal]: https://portal.azure.com
[lnk-fileupload-tutorial]: iot-hub-csharp-csharp-file-upload.md
[lnk-associate-storage]: iot-hub-devguide-file-upload.md#associate-an-azure-storage-account-with-iot-hub
[lnk-initialize]: iot-hub-devguide-file-upload.md#initialize-a-file-upload
[lnk-notify]: iot-hub-devguide-file-upload.md#notify-iot-hub-of-a-completed-file-upload
[lnk-service-notification]: iot-hub-devguide-file-upload.md#file-upload-notifications
[lnk-lifecycle]: iot-hub-devguide-messages-c2d.md#the-cloud-to-device-message-lifecycle
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-devguide-identities]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
