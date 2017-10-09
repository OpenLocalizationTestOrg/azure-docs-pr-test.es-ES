---
title: aaaOverview del borde de IoT de Azure | Documentos de Microsoft
description: "Describe Hola conceptos arquitectónicos clave en Azure IoT Edge como puertas de enlace, los módulos y los corredores de bolsa."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 32debc0d4f40cfd7f2cce7cf8c76b12ec18ee2dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a>Conceptos de arquitectura de Azure IoT Edge

Antes de examinar cualquier código de ejemplo o crear su propia puerta de enlace de campo con el borde de IoT, debe comprender los conceptos de clave de Hola que respaldan la arquitectura de hello del borde de IoT.

## <a name="iot-edge-modules"></a>Módulos de IoT Edge

Una puerta de enlace se crea con Azure IoT Edge mediante la creación y el ensamblado de *módulos de IoT Edge*. Utilizar los módulos de *mensajes* tooexchange datos entre sí. Un módulo recibe un mensaje, realiza alguna acción en él, opcionalmente transforma en un mensaje nuevo y, a continuación, publica para otros tooprocess de módulos. Existe la posibilidad de que algunos módulos solo produzcan nuevos mensajes y nunca procesen los mensajes entrantes. Una cadena de módulos, crea una canalización de procesamiento de datos con cada módulo realiza una transformación en los datos de hello en un punto de esa canalización.

![Cadena de módulos de puerta de enlace creada con Azure IoT Edge][1]

Borde de IoT contiene Hola de los componentes siguientes:

* Módulos escritos previamente que realizan funciones comunes de puerta de enlace.
* interfaces de Hello un desarrollador pueden utilizar módulos personalizados de toowrite.
* Hola toodeploy necesarios de infraestructura y ejecutar un conjunto de módulos.

Hola SDK proporciona una capa de abstracción que permite toobuild toorun de puertas de enlace en varios sistemas operativos y plataformas.

![Capa de abstracción de Azure IoT Edge][2]

## <a name="messages"></a>error de Hadoop

Aunque pensar en módulos de pasar mensajes tooeach otros es una manera cómoda de tooconceptualize cómo funciona una puerta de enlace, no con precisión refleja lo que sucede. Módulos de borde IoT usan un toocommunicate broker entre sí. Módulos publicación a broker toohello de mensajes (mediante patrones de mensajería como bus o de publicación/suscripción) y, a continuación, permiten Hola broker ruta Hola mensaje toohello módulos conectados tooit.

Un módulo usa hello **Broker_Publish** función toopublish un agente de toohello de mensajes. broker de Hello entrega módulo tooa de mensajes mediante la invocación de una función de devolución de llamada. Un mensaje consta de un conjunto de propiedades de clave/valor y del contenido que se pasa como un bloque de memoria.

![rol de Hola de hello Broker de borde de IoT de Azure][3]

## <a name="message-routing-and-filtering"></a>Enrutamiento y filtro de mensajes

Hay dos maneras de módulos de borde IoT correctos de toodirect mensajes toohello:

* Puede pasar un conjunto de vínculos se pueden pasar toohello broker para que sepa de broker de Hola Hola origen y el receptor para cada módulo.
* Un módulo puede filtrar según propiedades de Hola de mensaje de bienvenida.

Un módulo sólo debe actuar un mensaje si el mensaje de saludo está destinado. Los vínculos y el filtrado de mensajes crean de manera eficaz una canalización de mensajes.

## <a name="next-steps"></a>Pasos siguientes

toosee estos conceptos aplicados en un ejemplo que se puede ejecutar, consulte [arquitectura de explorar Azure IoT borde][lnk-hello-world].

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md