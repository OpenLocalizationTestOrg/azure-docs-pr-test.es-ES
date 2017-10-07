---
title: aaaAzure IoT soluciones preconfiguradas | Documentos de Microsoft
description: "Una descripción de hello Azure IoT preconfigurado soluciones y su arquitectura con recursos de tooadditional de vínculos."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 59009f37-9ba0-4e17-a189-7ea354a858a2
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: bd059d08ab458fdb0b6f49b3ac469db930dab09e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-azure-iot-suite-preconfigured-solutions"></a>¿Qué soluciones de Azure IoT conjunto preconfigurado de hello?

soluciones de Azure IoT conjunto preconfigurado de Hello son implementaciones de patrones comunes de solución de IoT que puede implementar tooAzure con su suscripción. Puede usar soluciones de hello preconfigurado:

* Como punto de partida para sus propias soluciones IoT.
* toolearn sobre patrones comunes de desarrollo y diseño de la solución de IoT.

Cada solución preconfigurada es una implementación completa, to-end que utiliza simulados telemetría toogenerate de dispositivos.

Puede descargar toocustomize de código fuente completo de Hola y extender Hola solución toomeet sus requisitos específicos de IoT.

> [!NOTE]
> toodeploy de hello soluciones preconfiguradas, visite [Microsoft Azure IoT Suite][lnk-azureiotsuite]. artículo de Hello [empezar a trabajar con soluciones de IoT preconfigurado hello] [ lnk-getstarted-preconfigured] proporciona más información acerca de cómo toodeploy y ejecute uno de Hola soluciones.

Hello tabla siguiente muestra cómo asignan las soluciones de hello toospecific IoT características:

| Solución | Ingesta de datos | Identidad del dispositivo | Administración de dispositivos | Comando y control | Reglas y acciones | Análisis predictivo |
| --- | --- | --- | --- | --- | --- | --- |
| [Supervisión remota][lnk-getstarted-preconfigured] |Sí |Sí |Sí |Sí |Sí |- |
| [Mantenimiento predictivo][lnk-predictive-maintenance] |Sí |Sí |- |Sí |Sí |Sí |
| [Fábrica conectada][lnk-getstarted-factory] |Sí |Sí |Sí |Sí |Sí |- |

* *Recopilación de datos*: entrada de datos en la nube a escala toohello.
* *Identidad del dispositivo*: administrar identidades de dispositivo único y controlar la solución de toohello de acceso de dispositivo.
* *Administración de dispositivos*: administre los metadatos de dispositivos y realice operaciones como reinicios de dispositivos y actualizaciones de firmware.
* *Comando y control*: toocause Hola dispositivo tootake una acción, enviar dispositivo tooa de mensajes de la nube de Hola.
* *Reglas y acciones*: tooact en los datos específicos de dispositivo a la nube, Hola solución back-end utiliza reglas.
* *Análisis predictivos*: Hola solución back-end analiza toopredict de datos del dispositivo a la nube cuando acciones específicas que deben tener lugar. Por ejemplo, análisis toodetermine de telemetría de motor de avión al motor de mantenimiento.

## <a name="remote-monitoring-preconfigured-solution-overview"></a>Información general sobre la solución preconfigurada de supervisión remota

Que hemos elegido toodiscuss Hola solución preconfigurada supervisión remoto en este artículo, ya que muestra muchos elementos de diseño comunes que Hola otro recurso compartido de soluciones.

Hello siguiente diagrama muestra elementos clave de Hola de hello remoto de solución de supervisión. Hello las secciones siguientes proporcionan más información acerca de estos elementos.

![Arquitectura de la solución preconfigurada de supervisión remota][img-remote-monitoring-arch]

## <a name="devices"></a>Dispositivos

Cuando se implementa Hola solución preconfigurada de supervisión remoto, cuatro dispositivos simulados son aprovisionados previamente en la solución de Hola que simula un dispositivo de enfriamiento. Estos dispositivos simulados tienen un modelo de temperatura y humedad integrado que emite telemetría. Estos dispositivos simulados se incluyen para hacer lo siguiente:

- Ilustrar el flujo de extremo a extremo de Hola de datos a través de la solución de Hola.
- Proporcionar un origen de telemetría conveniente.
- Proporcione un destino para métodos o los comandos si es un desarrollador de back-end mediante la solución de hello como punto de partida para una implementación personalizada.

dispositivos Hola simulado de solución de hello pueden responder toohello siguiendo las comunicaciones en la nube al dispositivo:

- *Métodos ([dirigir métodos][lnk-direct-methods])*: un método de comunicación bidireccional en un dispositivo conectado es toorespond esperada inmediatamente.
- *Comandos (en la nube al dispositivo mensajes)*: un método de comunicación unidireccional en un dispositivo recupera comando Hola desde una cola duradera.

Para ver una comparación de ambos enfoques distintos, consulte [Guía de comunicación de nube a dispositivo][lnk-c2d-guidance].

Cuando un dispositivo conecta primero tooIoT concentrador de solución de hello preconfigurado, envía un concentrador de toohello de mensaje de información de dispositivo. Este mensaje enumera los métodos de hello dispositivo Hola puede responder a. Hola solución preconfigurada de supervisión remoto, dispositivos simulados admiten estos métodos:

* *Iniciar la actualización de Firmware*: este método inicia una tarea asincrónica en hello dispositivo tooperform una actualización de firmware. tarea asincrónica de Hello usa el panel de propiedades notificado toodeliver estado actualizaciones toohello solución.
* *Reiniciar*: Hola simulada dispositivos tooreboot hace que este método.
* *FactoryReset*: este método desencadena una restablecimiento de fábrica en dispositivo simulado Hola.

Cuando un dispositivo conecta primero tooIoT concentrador de solución de hello preconfigurado, envía un concentrador de toohello de mensaje de información de dispositivo. Este mensaje enumera los comandos de hello dispositivo Hola puede responder a. Hola solución preconfigurada de supervisión remoto, dispositivos simulados admiten estos comandos:

* *Dispositivo de ping*: dispositivo Hola responde toothis comando con una confirmación. Este comando es útil para comprobar que dicho dispositivo Hola está todavía activa y realizando escuchas.
* *Iniciar la telemetría*: indica Hola dispositivo toostart enviar telemetría.
* *Detener la telemetría*: indica Hola dispositivo toostop enviar telemetría.
* *Cambiar punto establecido temperatura*: controles Hola temperatura simulada telemetría valores Hola dispositivo envíe. Este comando resulta útil para probar la lógica del back-end.
* *Telemetría de diagnóstico*: controla si el dispositivo de hello debería enviar temperatura externo hello como telemetría.
* *Cambio de estado de dispositivo*: establece la propiedad de metadatos de estado de dispositivo de Hola que Hola informes de dispositivos. Este comando resulta útil para probar la lógica del back-end.

Puede agregar más dispositivos simulados toohello solución que emiten Hola mismo telemetría y responden toohello mismos métodos y comandos.

Además tooresponding toocommands y métodos, solución de hello usa [: los gemelos de dispositivo][lnk-device-twin]. Los dispositivos utilizan dispositivos: los gemelos tooreport propiedad valores toohello solución back-end. panel de la solución de Hello usa valores de propiedad de dispositivo: los gemelos tooset toonew deseado en dispositivos. Por ejemplo, durante Hola firmware actualización proceso Hola simular dispositivos informes Hola de hello actualización de estado mediante propiedades notificados.

## <a name="iot-hub"></a>IoT Hub

En esta solución preconfigurada, hello instancia del centro de IoT corresponde toohello *puerta de enlace de nube* en típico [arquitectura de la solución de IoT][lnk-what-is-azure-iot].

Un centro de IoT recibe telemetría de dispositivos de hello en un solo punto de conexión. Un centro de IoT también mantiene los puntos de conexión específicos del dispositivo en cada dispositivo puede recuperar los comandos de Hola que se envían tooit.

Centro de IoT de Hola pone a disposición a través de telemetría de lado del servicio de hello leer extremo telemetría Hola recibido.

capacidad de administración de dispositivos de Hola de centro de IoT permite toomanage las propiedades de dispositivo de hello solución portal y programación de trabajos que realizan operaciones como:

- Reinicio de los dispositivos
- Cambio de los estados de los dispositivos
- Actualizaciones de firmware

## <a name="azure-stream-analytics"></a>Análisis de transmisiones de Azure

Hello solución preconfigurada usa tres [análisis de transmisiones de Azure] [ lnk-asa] flujo (ASA) trabajos toofilter Hola telemetría desde dispositivos de hello:

* *Trabajo de DeviceInfo* -centro de eventos de tooan de datos de resultados que enruta el registro de dispositivos de solución de dispositivo mensajes específicos del registro toohello. Este registro de dispositivos es una base de datos de Azure Cosmos DB. Estos mensajes se envían cuando conecta un dispositivo por primera vez o en respuesta tooa **cambiar el estado de dispositivo** comando.
* *Trabajo de telemetría* : envía todo el almacenamiento de blobs tooAzure telemetría sin procesar para un almacenamiento en frío y calcula las agregaciones de telemetría que se muestran en el panel de la solución de Hola.
* *Trabajo de reglas* : filtros hello secuencia de telemetría para los valores que superan los umbrales de las reglas y salidas Hola concentrador de eventos de tooan de datos. Cuando se desencadena una regla, vista de panel del portal de solución de hello muestra este evento como una nueva fila en la tabla de historial de alarma de Hola. Estas reglas también pueden desencadenar una acción según los valores de hello definidos en hello **reglas** y **acciones** vistas en el portal de solución de Hola.

En esta solución preconfigurada, Hola ASA trabajos forman parte de toohello **back-end de solución de IoT** en típico [arquitectura de la solución de IoT][lnk-what-is-azure-iot].

## <a name="event-processor"></a>procesador de eventos

En esta solución preconfigurada, el procesador de eventos de hello forma parte de hello **back-end de solución de IoT** en típico [arquitectura de la solución de IoT][lnk-what-is-azure-iot].

Hola **DeviceInfo** y **reglas** trabajos ASA envían sus centros de tooEvent de salida para la entrega de servicios back-end de tooother. Hola solución utiliza un [EventProcessorHost] [ lnk-event-processor] instancia, que se ejecuta un [WebJob][lnk-web-job], tooread mensajes de saludo de estos centros de eventos. Hola **EventProcessorHost** utiliza:
- Hola **DeviceInfo** tooupdate Hola dispositivo datos en la base de datos de base de datos de Cosmos Hola.
- Hola **reglas** datos tooinvoke Hola lógica aplicación y actualización Hola se muestran alertas en el portal de solución de Hola.

## <a name="device-identity-registry-device-twin-and-cosmos-db"></a>Registro de identidades de dispositivo, dispositivo gemelo y Cosmos DB

Cada centro de IoT incluye un [registro de identidades de dispositivo][lnk-identity-registry] que almacena las claves de dispositivo. Centro de IoT usa esta información autenticar los dispositivos: un dispositivo debe estar registrado y tiene una clave válida antes de poder conectar toohello concentrador.

A [gemelas dispositivo] [ lnk-device-twin] es un documento JSON administrado por hello centro de IoT. El dispositivo gemelo de un dispositivo contiene lo siguiente:

- Propiedad notificado enviada por centro de hello dispositivo toohello. Puede ver estas propiedades en el portal de solución de Hola.
- Propiedades que desee que desea toosend toohello dispositivo. Puede establecer estas propiedades en el portal de solución de Hola.
- Etiquetas que existen solo en gemelas de dispositivo de hello y no en el dispositivo de Hola. Puede usar estas listas de toofilter etiquetas de dispositivos en el portal de solución de Hola.

Esta solución utiliza los metadatos del dispositivo: los gemelos toomanage dispositivo. solución de Hello también usa un datos de dispositivo específica de la solución adicionales de toostore de base de datos de DB Cosmos como comandos de hello admitidos por cada historial de comandos hello y dispositivo.

solución de Hello también debe mantener información de hello en el registro de identidad de dispositivo Hola sincronizado con contenido de Hola de base de datos de base de datos de Cosmos Hola. Hola **EventProcessorHost** usa Hola datos de **DeviceInfo** sincronización de hello toomanage de trabajo de análisis de transmisiones.

## <a name="solution-portal"></a>Portal de solución

![Portal de solución][img-dashboard]

portal de solución de Hello es una interfaz de usuario basada en web que está en la nube toohello implementados como parte de la solución de hello preconfigurado. Le permite:

* Ver la telemetría y el historial de alarmas en un panel.
* Aprovisionar dispositivos nuevos.
* Administrar y supervisar los dispositivos.
* Enviar comandos toospecific dispositivos.
* Invocar métodos en dispositivos específicos.
* Administrar reglas y acciones.
* Programar trabajos toorun en uno o más dispositivos.

En esta solución preconfigurada, portal de solución de hello forma parte del programa Hola a **back-end de solución de IoT** y parte del programa Hola a **conectividad de procesamiento y empresarial** Hola típico [solución de IoT arquitectura][lnk-what-is-azure-iot].

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre las arquitecturas de solución de IoT, consulte el documento de [Servicios de IoT de Microsoft Azure: Arquitectura de referencia][lnk-refarch].

Ahora ya sabe qué es una solución preconfigurada es, puede empezar a implementando hello *supervisión remota* preconfigurado solución: [empezar a trabajar con soluciones de hello preconfigurado] [ lnk-getstarted-preconfigured].

[img-remote-monitoring-arch]: ./media/iot-suite-what-are-preconfigured-solutions/remote-monitoring-arch1.png
[img-dashboard]: ./media/iot-suite-what-are-preconfigured-solutions/dashboard.png
[lnk-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-event-processor]: ../event-hubs/event-hubs-programming-guide.md#event-processor-host
[lnk-web-job]: ../app-service-web/web-sites-create-web-jobs.md
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-getstarted-preconfigured]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-getstarted-factory]: iot-suite-connected-factory-overview.md
