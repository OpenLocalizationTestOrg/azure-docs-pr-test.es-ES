---
title: Tutorial de mantenimiento aaaPredictive | Documentos de Microsoft
description: "Un tutorial de un mantenimiento predictivo hello Azure IoT preconfigurado solución."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3c48a716-b805-4c99-8177-414cc4bec3de
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 900d6351019489a8e2f4b98908364e3bd14975c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-walkthrough"></a>Tutorial de la solución preconfigurada de mantenimiento predictivo

solución de un mantenimiento predictivo preconfigurado Hello es una solución de-to-end para un escenario empresarial que predice el punto de hello en el que un error es probable que toooccur. Puede utilizar esta solución preconfigurada de forma proactiva para actividades como, por ejemplo, la optimización del mantenimiento. solución de Hello combina servicios esenciales de conjunto de IoT de Azure, como centro de IoT, análisis de transmisiones y un [aprendizaje automático de Azure] [ lnk-machine-learning] área de trabajo. Esta área de trabajo contiene un modelo, basado en un conjunto de datos de ejemplo pública, toopredict Hola vida útil restante (RUL) de un motor de avión. solución de Hello totalmente implementa escenario empresarial de hello IoT como punto de partida para tooplan e implementar una solución que cumpla sus requisitos empresariales específicos.

## <a name="logical-architecture"></a>Arquitectura lógica

Hola siguiente diagrama describe los componentes lógicos de Hola de solución de hello preconfigurado:

![][img-architecture]

los elementos de Hello azul son servicios de Azure aprovisionados en la región de hello en la que implementó solución Hola preconfigurado. lista de Hola de regiones donde puede implementar soluciones de hello preconfigurado muestra de Hola [página aprovisionamiento][lnk-azureiotsuite].

elemento Hola verde es un dispositivo simulado que representa un motor de avión. Se puede obtener más información acerca de estos dispositivos simulados en hello pasos de la sección.

Hello elementos gris representan los componentes que implementan *la administración de dispositivos* capacidades. versión actual de Hola de solución de un mantenimiento predictivo preconfigurado hello no aprovisionar estos recursos. toolearn más información acerca de la administración de dispositivos, consulte toohello [solución preconfigurada de supervisión remota][lnk-remote-monitoring].

## <a name="simulated-devices"></a>Dispositivos simulados

En la solución Hola preconfigurado, un dispositivo simulado representa un motor de avión. solución de Hola se aprovisiona con dos motores que se asignan tooa único avión. Cada motor emite cuatro tipos de telemetría: Sensor 9, 11 de Sensor, Sensor 14 y 15 del Sensor de proporcionan datos de hello necesarias para Hola aprendizaje automático modelo toocalculate Hola RUL para motor Hola. Cada dispositivo simulado envía Hola después telemetría mensajes tooIoT concentrador:

*Recuento de ciclos*. Un ciclo representa un vuelo completo con una duración de entre dos y diez horas. Durante el vuelo de hello, los datos de telemetría se capturan cada media hora.

*Telemetría*. Existen cuatro sensores que representan atributos de motor. sensores de Hello genéricamente se etiquetan Sensor 9, Sensor 11, Sensor 14 y 15 de Sensor. Estos cuatro sensores representan resultados útiles de telemetría suficiente de tooobtain de modelo RUL Hola. modelo Hola que se usa en soluciones de hello preconfigurado se crea a partir de un conjunto de datos público que incluye datos del sensor del motor real. Para obtener más información sobre cómo se creó el modelo de Hola de conjunto de datos original de hello, vea hello [Cortana Intelligence Galería predictivo mantenimiento plantilla][lnk-cortana-analytics].

dispositivos de Hello simulado pueden administrar Hola siga los comandos enviados desde el centro de IoT de hello en soluciones de hello:

| Comando | Description |
| --- | --- |
| StartTelemetry |Estado de simulación de Hola Hola a controles.<br/>Dispositivo de hello inicia enviar telemetría |
| StopTelemetry |Estado de simulación de Hola Hola a controles.<br/>Se detiene Hola enviar telemetría de dispositivo |

Centro de IoT proporciona la confirmación de los comandos del dispositivo.

## <a name="azure-stream-analytics-job"></a>Trabajo de Análisis de transmisiones de Azure

**Trabajo: Telemetría** opera en hello dispositivo telemetría secuencia entrante con dos instrucciones:

* Hola primero selecciona todos los telemetría desde dispositivos de Hola y envía este almacenamiento de datos tooblob. Desde aquí, se visualiza en la aplicación web de hello.
* Hola segundo calcula sensor promedio valores a través de una ventana deslizante de dos minutos y envía estos datos a través de tooan de concentrador de eventos de hello **procesador de eventos**.

## <a name="event-processor"></a>procesador de eventos
Hola **host procesador de eventos** se ejecuta en un trabajo Web de Azure. Hola **procesador de eventos** toma los valores de sensor promedio de hello en un ciclo completado. A continuación, pasa esos tooan API que expone toocalculate Hola RUL de modelo entrenado para un motor de valores. Hola API se expone un área de trabajo de aprendizaje automático que se proporciona como parte de la solución de Hola.

## <a name="machine-learning"></a>Machine Learning
componente de aprendizaje automático de Hello usa un modelo derivado de los datos recopilados de los motores del avión real. Puede navegar por área de trabajo de aprendizaje automático de toohello desde icono de hello en hello [azureiotsuite.com] [ lnk-azureiotsuite] página para su solución de aprovisionamiento. Hello mosaico está disponible cuando solución hello es Hola **listo** estado.


## <a name="next-steps"></a>Pasos siguientes
Ahora que ha visto los componentes clave de Hola de solución de un mantenimiento predictivo preconfigurado hello, puede que desee toocustomize se. Consulte [Personalizar una solución preconfigurada][lnk-customize].

También puede explorar algunas de hello otras características y capacidades de hello IoT preconfigurado soluciones:

* [Preguntas más frecuentes sobre el Conjunto de aplicaciones de IoT][lnk-faq]
* [Seguridad de IoT de hello masa][lnk-security-groundup]

[img-architecture]: media/iot-suite-predictive-walkthrough/architecture.png

[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-cortana-analytics]: http://gallery.cortanaintelligence.com/Collection/Predictive-Maintenance-Template-3
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/