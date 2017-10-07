---
title: puerta de enlace de protocolo de aaaAzure IoT | Documentos de Microsoft
description: "¿Cómo toouse un IoT de Azure protocolo capacidades de centro de IoT tooextend de puerta de enlace y protocolo compatibilidad tooenable dispositivos tooconnect tooyour concentrador mediante protocolos no admitidos por centro de IoT de forma nativa."
services: iot-hub
documentationcenter: 
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 555e59ae-3136-4533-8ba8-f3a3b6acf648
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.openlocfilehash: 9cfed30149672d8f7e021a9899192105bbcdd400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# Compatibilidad con protocolos adicionales para centro de IoT Hub
Centro de IoT de Azure admite de forma nativa la comunicación a través de protocolos de hello MQTT, AMQP y HTTP. En algunos casos, los dispositivos o puertas de enlace de campo podrían no ser capaz de toouse uno de estos protocolos estándar y requerirán la adaptación de protocolo. En esos casos, puede usar una puerta de enlace personalizada. Una puerta de enlace personalizado puede habilitar la adaptación de protocolo para extremos de centro de IoT Hola tráfico tooand centro de IoT de protocolo de puente. Puede usar hello [puerta de enlace de IoT de Azure protocolo](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md) como una adaptación de protocolo de puerta de enlace personalizado tooenable para el centro de IoT.

## Puerta de enlace de protocolos de IoT de Azure
puerta de enlace de protocolo de Hello IoT de Azure es un marco para la adaptación de protocolo que está diseñado para la comunicación de dispositivos de bidireccional con el centro de IoT de gran escala. puerta de enlace de protocolo de Hello es un componente de acceso directo que acepta conexiones de dispositivos a través de un protocolo específico. Une Hola tráfico tooIoT concentrador en AMQP 1.0. puerta de enlace de protocolo de Hello IoT de Azure está disponible como una flexibilidad de tooprovide del proyecto de software de código abierto para agregar compatibilidad con distintos protocolos y las versiones de protocolo.

Puede implementar la puerta de enlace de protocolo de hello en Azure de una manera altamente escalable mediante Azure Service Fabric, los roles de trabajo de servicios en la nube o máquinas virtuales de Windows. Además, la puerta de enlace de protocolo de hello puede implementarse en entornos locales, como puertas de enlace de campo.

puerta de enlace de protocolo de Hello IoT de Azure incluye un adaptador de protocolo MQTT que permite toocustomize Hola comportamiento del protocolo MQTT si es necesario. Puesto que el centro de IoT proporciona compatibilidad integrada para el protocolo de hello MQTT v3.1.1, sólo puede utilizar adaptador de protocolo de hello MQTT si son necesarios las personalizaciones de protocolo o requisitos específicos para una funcionalidad adicional.

adaptador de Hello MQTT también muestra el modelo de programación de hello para la creación de adaptadores de protocolo para otros protocolos. Además, modelo de programación de la puerta de enlace del protocolo de hello IoT de Azure permite especializados tooplug en componentes personalizados para su procesamiento como autenticación personalizada, transformaciones de mensajes, compresión y descompresión o cifrado y descifrado de tráfico entre los dispositivos de Hola y centro de IoT.

Para mayor flexibilidad, la puerta de enlace de protocolo de Hola y la implementación de MQTT se proporcionan en un proyecto de software de código abierto. Esto le permite la implementación de hello toocustomize según sea necesario.

## Pasos siguientes
toolearn más información acerca de la puerta de enlace de protocolo de hello IoT de Azure y cómo toouse e implementar como parte de la solución de IoT, consulte:

* [Repositorio de puerta de enlace de protocolos de IoT de Azure en GitHub](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md)
* [Guía para desarrolladores de puerta de enlace de protocolos de IoT de Azure](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/docs/DeveloperGuide.md)

toolearn más información acerca de la planeación de la implementación del centro de IoT, vea:

* [Comparación con Event Hubs][lnk-compare]
* [Escalado, alta disponibilidad y recuperación ante desastres][lnk-scaling]
* [Guía para desarrolladores de IoT Hub][lnk-devguide]

[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
