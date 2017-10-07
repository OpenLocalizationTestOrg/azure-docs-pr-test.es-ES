---
title: "metadatos de la información de aaaDevice Hola remoto de solución de supervisión | Documentos de Microsoft"
description: "Una descripción de hello Azure IoT preconfigurado supervisión remota de solución y su arquitectura."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 8387b98b8b2ae4934b0c900bc4df37dc17337c60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a>Metadatos de información de dispositivo en hello solución preconfigurada de supervisión remota

Hola Suite de IoT de Azure remoto solución preconfigurada de supervisión muestra un enfoque para administrar los metadatos del dispositivo. En este artículo se describe el enfoque de hello esta solución toma tooenable toounderstand:

* ¿Qué solución de Hola de metadatos de dispositivo se almacena.
* Cómo la solución de hello administra Hola metadatos del dispositivo.

## <a name="context"></a>Context

Hello supervisión remota preconfigurado solución usa [centro de IoT de Azure] [ lnk-iot-hub] tooenable su toohello de datos de dispositivos toosend en la nube. solución de Hello almacena información acerca de los dispositivos en tres ubicaciones diferentes:

| Ubicación | Información almacenada | Implementación |
| -------- | ------------------ | -------------- |
| Registro de identidad | Identificador de dispositivo, claves de autenticación, estado habilitado | TooIoT incorporada concentrador |
| Dispositivos gemelos | Metadatos: propiedades notificadas, propiedades deseadas, etiquetas | TooIoT incorporada concentrador |
| Cosmos DB | Historial de comandos y métodos | Personalizado para la solución |

Centro de IoT incluye un [del registro de la identidad de dispositivo] [ lnk-identity-registry] toomanage acceso tooan centro de IoT y utiliza [: los gemelos de dispositivo] [ lnk-device-twin] toomanage metadatos del dispositivo . También hay un *registro de dispositivo* específico de la solución de supervisión remota que almacena el historial de comandos y métodos. Hola remoto de supervisión de solución usa un [Cosmos DB] [ lnk-docdb] tooimplement de base de datos un almacén personalizado para el historial de comandos y método.

> [!NOTE]
> Hola solución preconfigurada de supervisión remoto mantiene del registro de identidad de dispositivo de hello sincronizada con la información de hello en la base de datos de base de datos de Cosmos Hola. Ambos utilizan Hola mismo toouniquely de Id. de dispositivo identificar cada dispositivo conectado tooyour centro de IoT.

## <a name="device-metadata"></a>Metadatos del dispositivo

Centro de IoT mantiene un [gemelas dispositivo] [ lnk-device-twin] para cada dispositivo simulado y físico conectado tooa remoto de solución de supervisión. solución de Hello usa dispositivos: los gemelos toomanage Hola metadatos asociados con los dispositivos. Un gemelas de dispositivo es un documento JSON mantenido por centro de IoT y solución hello usa Hola IoT Hub API toointeract con: los gemelos de dispositivo.

Un dispositivo gemelo almacena tres tipos de metadatos:

- *Notifica propiedades* se envían centro de IoT tooan por un dispositivo. Hola remoto de solución de supervisión, dispositivos simulados envían propiedades notificados durante el inicio y en respuesta demasiado**cambiar el estado de dispositivo** comandos y métodos. Puede ver propiedades notificados en hello **lista de dispositivos** y **detalles del dispositivo** en el portal de solución de Hola. Las propiedades notificadas son de solo lectura.
- *Las propiedades adecuadas* se recuperan de centro de IoT hello mediante dispositivos. Es responsabilidad de Hola de hello dispositivo toomake cambiar cualquier configuración necesaria en el dispositivo de Hola. También es responsabilidad de hello del concentrador de hello dispositivo tooreport Hola cambio toohello espera como una propiedad notificada. Puede establecer un valor de propiedad a través del portal de solución de Hola.
- *Etiquetas* solo existen en gemelas de dispositivo de Hola y nunca se sincronizan con un dispositivo. Puede establecer valores de etiqueta en el portal de solución de Hola y usarlas cuando se aplica un filtro lista Hola de dispositivos. solución de Hello también utiliza un toodisplay de icono de etiqueta tooidentify Hola para un dispositivo en el portal de solución de Hola.

En el ejemplo se notifica las propiedades desde dispositivos de hello simulado incluyen fabricante, número de modelo, latitud y longitud. Dispositivos simulados también devuelvan lista Hola de métodos admitidos como una propiedad notificada.

> [!NOTE]
> Hello dispositivo simulado código solo usa hello **Desired.Config.TemperatureMeanValue** y **Desired.Config.TelemetryInterval** hello tooupdate de propiedades que desee notificado propiedades devuelve tooIoT concentrador. Todos los demás cambios de propiedades deseadas se omiten.

Un documento de JSON de metadatos de información de dispositivo almacenado en base de datos base de datos de Cosmos del registro de dispositivos de hello tiene Hola siguiendo estructura:

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> Información del dispositivo también puede incluir metadatos toodescribe Hola telemetría Hola dispositivo envía tooIoT concentrador. solución de supervisión remoto Hello usa este toocustomize de metadatos de telemetría cómo muestra el panel de hello [telemetría dinámica][lnk-dynamic-telemetry].

## <a name="lifecycle"></a>Ciclo de vida

Cuando se crea por primera vez un dispositivo en el portal de solución de hello, solución de hello crea una entrada de hello comandos de toostore de base de datos de base de datos de Cosmos y el historial de método. En este momento, solución de hello también crea una entrada para el dispositivo de hello en el registro de identidad de dispositivo de hello, que genera Hola claves Hola dispositivo usa tooauthenticate con centro de IoT. También crea un dispositivo gemelo.

Cuando un dispositivo conecta primero toohello solución, envía propiedades notificados y un mensaje de información de dispositivo. Hola informó de valores de propiedad se guardan automáticamente en gemelas de dispositivo de Hola. Hola notifica las propiedades incluyen el fabricante del dispositivo de hello, número de modelo, número de serie y una lista de los métodos admitidos. mensaje de información de dispositivo de Hello incluye la lista de Hola de comandos de hello es compatible con dispositivos de hello incluida información acerca de los parámetros del comando. Cuando la solución de hello recibe este mensaje, actualiza información del dispositivo hello en la base de datos de base de datos de Cosmos Hola.

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a>Ver y editar la información del dispositivo en el portal de solución de Hola

lista de dispositivos en el portal de solución de hello Hello muestra hello siguientes propiedades del dispositivo como columnas de forma predeterminada: **estado**, **DeviceId**, **fabricante**, **Número modelo**, **número de serie**, **Firmware**, **plataforma**, **procesador**y  **Instalado RAM**. Puede personalizar las columnas de hello haciendo clic en **editor columna**. propiedades del dispositivo de Hola **latitud** y **longitud** unidad ubicación Hola Hola Bing Maps en el panel de Hola.

![Editor de columnas en la lista de dispositivos][img-device-list]

Hola **detalles del dispositivo** panel en el portal de solución de hello, puedes editar etiquetas y propiedades que desee (notificada propiedades son de sólo lectura).

![Panel de detalles del dispositivo][img-device-edit]

Puede usar tooremove de portal de solución de hello un dispositivo de la solución. Cuando se quita un dispositivo, solución de hello quita la entrada de dispositivo de Hola desde el registro de identidad y luego elimina a gemelas de dispositivo de Hola. solución de Hello también quita el dispositivo de toohello relacionadas de información de base de datos de base de datos de Cosmos Hola. Para poder quitar un dispositivo, debe deshabilitarlo.

![Quitar dispositivo][img-device-remove]

## <a name="device-information-message-processing"></a>Procesamiento de mensajes de información de dispositivo

Los mensajes de información de dispositivo enviados por un dispositivo son distintos de los mensajes de telemetría. Mensajes de información de dispositivo incluyen comandos Hola a que un dispositivo puede responder y todo el historial del comando. Centro de IoT de sí mismo no tiene ningún conocimiento de los metadatos de hello contenidos en un mensaje de información de dispositivo y procesos Hola mensaje Hola igual que procesa los mensajes del dispositivo a la nube. Hola remoto de supervisión de la solución, un [análisis de transmisiones de Azure] [ lnk-stream-analytics] trabajo (ASA) lee mensajes de saludo de centro de IoT. Hola **DeviceInfo** filtros para los mensajes que contengan de trabajo de análisis de transmisiones **"ObjectType": "DeviceInfo"** y los reenvía toohello **EventProcessorHost** host instancia que se ejecuta en un trabajo web. Lógica de hello **EventProcessorHost** instancia utiliza registro de hello dispositivo identificador toofind Hola DB Cosmos para hello dispositivo y actualización Hola registros específicos.

> [!NOTE]
> Un mensaje de información de dispositivo es un mensaje estándar del dispositivo a la nube. solución de Hello distingue entre mensajes de información de dispositivo y telemetría mediante consultas ASA.

## <a name="next-steps"></a>Pasos siguientes

Ahora que has terminado de aprender cómo personalizar soluciones de hello preconfigurado, puede explorar algunas de hello otras características y capacidades de hello IoT preconfigurado soluciones:

* [Información general de la solución preconfigurada de mantenimiento predictivo][lnk-predictive-overview]
* [Preguntas más frecuentes sobre el Conjunto de aplicaciones de IoT][lnk-faq]
* [Seguridad de IoT de hello masa][lnk-security-groundup]

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
