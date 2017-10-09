---
title: "Tutorial de solución de supervisión preconfigurado aaaRemote | Documentos de Microsoft"
description: "Una descripción de hello Azure IoT preconfigurado supervisión remota de solución y su arquitectura."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a>Tutorial de la solución preconfigurada de supervisión remota

Hola supervisión remota de IoT Suite [preconfigurado solución] [ lnk-preconfigured-solutions] es una implementación de un extremo a extremo de supervisión soluciones para varias máquinas que se ejecutan en ubicaciones remotas. solución de Hello combina servicios de Azure clave tooprovide una implementación genérica de escenario empresarial de Hola. Puede usar soluciones de hello como punto de partida para su propia implementación y [personalizar] [ lnk-customize] toomeet sus propios requisitos empresariales específicos.

Este artículo le guiará a través de algunos de los elementos clave de Hola de tooenable de solución de supervisión remota de hello toounderstand su funcionamiento. Esta información le ayuda a:

* Solucionar problemas de solución de Hola.
* Planear cómo toocustomize toohello solución toomeet sus propios requisitos específicos. 
* Diseñar una solución de IoT propia que utilice servicios de Azure.

## <a name="logical-architecture"></a>Arquitectura lógica

Hola siguiente diagrama describe los componentes lógicos de Hola de solución de hello preconfigurado:

![Arquitectura lógica](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a>Dispositivos simulados

En la solución Hola preconfigurado, dispositivo simulado de Hola representa un dispositivo de enfriamiento (como un acondicionador de aire de creación o la unidad de control de utilidad aire). Al implementar soluciones de hello preconfigurado, aprovisionar automáticamente cuatro dispositivos simulados que se ejecutan en un [WebJob de Azure][lnk-webjobs]. dispositivos de Hello simulado facilitan tooexplore Hola comportamiento de hello solución sin Hola necesidad toodeploy los dispositivos físicos. toodeploy un dispositivo físico real, vea hello [conectar su toohello de dispositivo remoto solución preconfigurada de supervisión] [ lnk-connect-rm] tutorial.

### <a name="device-to-cloud-messages"></a>Mensajes de dispositivo a nube

Cada dispositivo simulado puede enviar Hola después tooIoT de tipos de mensaje concentrador:

| Message | Description |
| --- | --- |
| Inicio |Cuando se inicia el dispositivo de hello, envía una **información del dispositivo** mensaje que contiene información sobre ella misma toohello back-end. Estos datos incluyen el Id. de dispositivo de hello y una lista de comandos de Hola y métodos Hola admite el dispositivo. |
| Presencia |Un dispositivo envía periódicamente un **presencia** tooreport de mensajes si el dispositivo Hola puede detectar la presencia de Hola de un sensor. |
| Telemetría |Un dispositivo envía periódicamente un **telemetría** mensaje que notifica simulados valores de temperatura de Hola y humedad procedentes de dispositivos de Hola de simular sensores. |

> [!NOTE]
> solución de Hello almacena la lista de Hola de comandos admitidos por dispositivo de hello en una base de datos de la base de datos de Cosmos y no en gemelas de dispositivo de Hola.

### <a name="properties-and-device-twins"></a>Propiedades y dispositivos gemelos

dispositivos simulados Hello envían Hola después toohello de propiedades de dispositivo [gemelas] [ lnk-device-twins] en el centro de IoT hello como *notificado propiedades*. dispositivo envía Hello notificado propiedades en el inicio y en respuesta tooa **cambio de estado de dispositivo** comando o un método.

| Propiedad | Propósito |
| --- | --- |
| Config.TelemetryInterval | Dispositivo de Hola de frecuencia (segundos) envía telemetría |
| Config.TemperatureMeanValue | Especifica el valor medio de Hola para telemetría de temperatura de hello simulada |
| Device.DeviceID |Id. que se proporcionan o se asigna cuando se crea un dispositivo de solución de Hola |
| Device.DeviceState | Estado notificado por dispositivo de Hola |
| Device.CreatedTime |Dispositivo de Hola de tiempo se creó en soluciones de Hola |
| Device.StartupTime |Se inició el dispositivo de Hola de tiempo |
| Device.LastDesiredPropertyChange |cambiar el número de versión de Hello de la última propiedad deseado de Hola |
| Device.Location.Latitude |Ubicación de latitud de dispositivo de Hola |
| Device.Location.Longitude |Ubicación de la longitud del dispositivo de Hola |
| System.Manufacturer |Fabricante del dispositivo |
| System.ModelNumber |Número de modelo de dispositivo de Hola |
| System.SerialNumber |Número de serie del dispositivo de Hola |
| System.FirmwareVersion |Versión actual de firmware de dispositivo de Hola |
| System.Platform |Arquitectura de la plataforma de dispositivo de Hola |
| System.Processor |Dispositivo en ejecución Hola procesador |
| System.InstalledRAM |Cantidad de RAM instalada en el dispositivo de Hola |

simulador de Hello propaga estas propiedades en los dispositivos simulados con valores de ejemplo. Cada vez simulador Hola Inicializa un dispositivo simulado, el dispositivo de hello notifica Hola metadatos previamente definidos tooIoT concentrador como propiedades notificados. Propiedades incluidos solo pueden actualizarse por dispositivo de Hola. toochange una propiedad incluida, se establece una propiedad deseada en el portal de solución. Es responsabilidad de hello de dispositivo de Hola para:

1. Recuperar de forma periódica propiedades deseadas Hola centro de IoT.
2. Actualice su configuración con el valor de propiedad de hello deseado.
3. Enviar nuevo centro de atrás toohello valor Hola como una propiedad notificada.

En el panel de la solución de hello, puede usar *deseado propiedades* tooset propiedades en un dispositivo mediante el uso de hello [gemelas dispositivo][lnk-device-twins]. Normalmente, un dispositivo lee un valor de propiedad de hello concentrador tooupdate que cambian su estado interno y Hola de informe como una propiedad notificada.

> [!NOTE]
> Hello dispositivo simulado código solo usa hello **Desired.Config.TemperatureMeanValue** y **Desired.Config.TelemetryInterval** hello tooupdate de propiedades que desee notificado propiedades devuelve tooIoT concentrador. Se omiten todas las demás solicitudes de cambio de la propiedad deseada en el dispositivo simulado de Hola.

### <a name="methods"></a>Métodos

Hello dispositivos simulados pueden controlar Hola siguiendo métodos ([dirigir métodos][lnk-direct-methods]) se invoca desde el portal de solución de Hola a través del centro de IoT de hello:

| Método | Descripción |
| --- | --- |
| InitiateFirmwareUpdate |Indica a Hola dispositivo tooperform una actualización de firmware |
| Reboot |Indica a Hola dispositivo tooreboot |
| FactoryReset |Indica a Hola dispositivo tooperform restablecer una fábrica |

Algunos métodos usan propiedades notificado tooreport en curso. Por ejemplo, hello **InitiateFirmwareUpdate** método simula la ejecución actualización Hola asincrónicamente en el dispositivo de Hola. método Hello devuelve inmediatamente en el dispositivo de hello, mientras continúa la tarea asincrónica Hola volver las actualizaciones de estado de toosend toohello solución panel mediante informó de propiedades.

### <a name="commands"></a>Comandos:

dispositivos de Hello simulado pueden administrar Hola después de comandos (en la nube al dispositivo mensajes) enviados desde el portal de solución de Hola a través del centro de IoT de hello:

| Comando | Description |
| --- | --- |
| PingDevice |Envía una *ping* toohello toocheck de dispositivo está activo |
| StartTelemetry |Dispositivo de hello inicia enviar telemetría |
| StopTelemetry |Dispositivo de Hola se detiene en el envío de telemetría |
| ChangeSetPointTemp |Cambia el valor punto establecido Hola alrededor de qué Hola se generan datos aleatorios |
| DiagnosticTelemetry |Desencadenadores Hola toosend de simulador de dispositivo un valor de telemetría adicionales (externalTemp) |
| ChangeDeviceState |Cambia una propiedad de estado extendido para dispositivo hello y envía el mensaje de información de dispositivo de hello de dispositivo de Hola |

> [!NOTE]
> Para ver una comparación de estos comandos (mensajes de la nube al dispositivo) y métodos (métodos directos), consulte [Guía de comunicación de nube a dispositivo][lnk-c2d-guidance].

## <a name="iot-hub"></a>IoT Hub

Hola [centro de IoT] [ lnk-iothub] introduce los datos enviados desde dispositivos de hello en nube de Hola y hace que los trabajos de análisis de transmisiones de Azure (ASA) toohello disponibles. Cada trabajo ASA de flujo utiliza una centro de IoT consumidor grupo tooread hello secuencia independiente de los mensajes de los dispositivos.

Hola centro de IoT de solución de hello también:

- Mantiene un registro de la identidad que almacena los identificadores de Hola y claves de autenticación de todos los dispositivos de hello permitidas tooconnect toohello portal. Puede habilitar y deshabilitar dispositivos a través del registro de identidad de Hola.
- Envía comandos tooyour dispositivos en nombre de portal de solución de Hola.
- Invoca los métodos de los dispositivos en nombre de portal de solución de Hola.
- Mantiene los dispositivos gemelos para todos los dispositivos registrados. Un gemelas dispositivo almacena valores de propiedades de hello notificados por un dispositivo. Un gemelas dispositivo también almacena las propiedades deseadas, establecidas en el portal de solución de hello, para hello dispositivo tooretrieve cuando se conecta a continuación.
- Programaciones de trabajos tooset propiedades para varios dispositivos o para invocar métodos en varios dispositivos.

## <a name="azure-stream-analytics"></a>Análisis de transmisiones de Azure

Hola remoto de supervisión de solución, [análisis de transmisiones de Azure] [ lnk-asa] (ASA) envía los mensajes de dispositivo recibidos por componentes de hello IoT hub tooother back-end para el procesamiento o de almacenamiento. Los distintos trabajos ASA realizan funciones específicas basadas en contenido de Hola de mensajes de saludo.

**Trabajo 1: Información del dispositivo** filtra los mensajes de información de dispositivo de la secuencia de mensajes de Hola entrantes y los envía el punto de conexión de tooan centro de eventos. Un dispositivo envía mensajes de información de dispositivo en el inicio y de respuesta tooa **SendDeviceInfo** comando. Este trabajo utiliza Hola después tooidentify de definición de consulta **información del dispositivo** mensajes:

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

Este trabajo envía su centro de eventos de salida tooan para su posterior procesamiento.

**Trabajo 2: reglas** evalúa los valores de telemetría de temperatura y humedad entrantes según los umbrales por dispositivo. Valores de umbral se establecen en el editor de reglas de hello disponible en el portal de solución de Hola. Cada par de valor/dispositivo se almacena en la marca de tiempo de un blob que se lee en Análisis de transmisiones como **datos de referencia**. trabajo Hola compara cualquier valor no vacío con umbral de conjunto de hello de dispositivo de Hola. Si se supera hello ' >' de condición, Hola trabajo devuelva un **alarma** evento que indica que ese umbral Hola se supera y ofrecen dispositivo hello, valor y los valores de marca de tiempo. Este trabajo utiliza Hola siguientes mensajes de telemetría de tooidentify de definición de consulta que deben desencadenar una alarma:

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

Hola trabajo envía su centro de eventos de salida tooan para su posterior procesamiento y evita que los detalles de cada alerta tooblob almacenamiento donde portal de solución de hello puede leer la información de alertas de Hola.

**Tarea 3: Telemetría** funciona en flujo de telemetría de dispositivo entrante de Hola de dos maneras. Hola envía primero todos los mensajes de telemetría Hola dispositivos toopersistent almacenamiento de blobs para almacenamiento a largo plazo. Hola segundo calcula humedad promedio, mínimo y máximo valores a través de una ventana deslizante de cinco minutos y envía este almacenamiento de datos tooblob. portal de solución de Hello lee los datos de telemetría de Hola de gráficos de Hola de toopopulate de almacenamiento de blobs. Este trabajo utiliza Hola después de la definición de la consulta:

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a>Centros de eventos

Hola **información del dispositivo** y **reglas** trabajos ASA muestran su datos tooEvent concentradores tooreliably al día en toohello **procesador de eventos** ejecutando Hola trabajo Web.

## <a name="azure-storage"></a>Almacenamiento de Azure

solución de Hello utiliza toopersist de almacenamiento de blobs de Azure todos los datos de telemetría resumido y sin formato de Hola desde dispositivos de hello en soluciones de Hola. portal de Hello lee los datos de telemetría de Hola de gráficos de Hola de toopopulate de almacenamiento de blobs. toodisplay alertas, portal de solución de hello lee Hola datos desde almacenamiento de blobs que registra cuando Hola de telemetría valores superados configura valores de umbral. solución de Hello también utiliza valores blob almacenamiento toorecord Hola umbral establecido en el portal de solución de Hola.

## <a name="webjobs"></a>Trabajos web

Además simuladores de dispositivos de toohosting hello, Hola trabajos Web de solución de hello también Hola host **procesador de eventos** ejecutando en un trabajo Web de Azure que controla las respuestas de comando. Usa el comando respuesta mensajes tooupdate Hola dispositivo comando Historial (almacenado en la base de datos de base de datos de Cosmos hello).

## <a name="cosmos-db"></a>Cosmos DB

solución de Hello utiliza una base de datos de Cosmos base de datos toostore información sobre las Hola dispositivos toohello conectado solución. Esta información incluye el historial de Hola de comandos enviados toodevices desde el portal de solución de Hola y de los métodos invocados desde el portal de solución de Hola.

## <a name="solution-portal"></a>Portal de solución

portal de solución de Hello es una aplicación web que se implementa como parte de la solución de hello preconfigurado. páginas de clave de Hello en el portal de solución de hello son lista de dispositivos de Hola y el panel de Hola.

### <a name="dashboard"></a>Panel

Esta página de aplicación web de hello usa controles de javascript de Power BI (consulte [repositorio de PowerBI-visuals](https://www.github.com/Microsoft/PowerBI-visuals)) los datos de telemetría de hello toovisualize desde dispositivos de Hola. solución de Hello utiliza Hola ASA telemetría trabajo toowrite Hola telemetría tooblob almacenamiento de datos.

### <a name="device-list"></a>Lista de dispositivos

Desde esta página en el portal de solución de hello hacer lo siguiente:

* Aprovisionar un dispositivo nuevo. Esta acción establece el Id. de dispositivo único hello y genera la clave de autenticación de Hola. Escribe información acerca de Hola Hola de tooboth de dispositivo del registro de identidad de centro de IoT y base de datos de base de datos de Cosmos de hello específica de la solución.
* Administrar las propiedades del dispositivo. Esta acción incluye las propiedades de visualización existentes y la actualización con nuevas propiedades.
* Enviar dispositivo tooa de comandos.
* Ver el historial del comando de Hola para un dispositivo.
* Habilitar y deshabilitar dispositivos.

## <a name="next-steps"></a>Pasos siguientes

Hello entradas de blog de TechNet siguientes proporcionan más detalles sobre Hola remoto solución preconfigurada de supervisión:

* [Supervisión remota de IoT Suite - bajo el paraguas de Hola:](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [IoT Suite - Remote Monitoring - Adding Live and Simulated Devices (Conjunto de aplicaciones de IoT, Supervisión remota: Incorporación de dispositivos activos y simulados)](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

Puede seguir introducción con Suite IoT leyendo Hola siguientes artículos:

* [Conectar su toohello de dispositivo remoto solución preconfigurada de supervisión][lnk-connect-rm]
* [Permisos en el sitio de hello azureiotsuite.com][lnk-permissions]

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
