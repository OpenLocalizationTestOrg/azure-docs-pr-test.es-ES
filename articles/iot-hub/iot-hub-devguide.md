---
title: "Guía de aaaDeveloper para el centro de IoT de Azure | Documentos de Microsoft"
description: "Guía del desarrollador de Hello centro de IoT de Azure incluye las discusiones de los puntos de conexión, seguridad, del registro de identidad de hello, administración de dispositivos, métodos directos,: los gemelos de dispositivo, cargas de archivos, trabajos, Hola lenguaje de consultas del centro de IoT y mensajería."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: d534ff9d-2de5-4995-bb2d-84a02693cb2e
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 2d3f18399e4cef6f9c4850a5caeb170a2d091a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-developer-guide"></a>Guía del desarrollador del Centro de IoT de Azure

IoT Hub de Azure es un servicio totalmente administrado que permite la comunicación bidireccional confiable y segura entre millones de dispositivos y una solución de back-end.

IoT Hub de Azure le proporciona:

* Comunicaciones seguras a través del uso de credenciales de seguridad para cada dispositivo y el control de acceso.
* Varias opciones de comunicación a gran escala de dispositivo a la nube y de la nube a dispositivo.
* Almacenamiento consultable de la información de estado y los metadatos de cada dispositivo.
* Conectividad sencilla de los dispositivos con bibliotecas de dispositivo para los lenguajes más populares de Hola y plataformas.

Esta guía del desarrollador de centro de IoT incluye Hola siguientes artículos:

* [Device-to-cloud communication guidance][lnk-d2c-guidance] (Guía de comunicación de dispositivo a nube) le permite elegir entre los mensajes del dispositivo a la nube, las propiedades notificadas del dispositivo gemelo y la carga de archivos.
* [Guía de comunicación de nube a dispositivo][lnk-c2d-guidance] le ayuda a elegir entre métodos directos, las propiedades preferidas del dispositivo gemelo y los mensajes de la nube al dispositivo.
* [Dispositivo para la nube y en la nube al dispositivo de mensajería con centro de IoT] [ devguide-messaging] describe Hola características de mensajería (dispositivo a la nube y en la nube al dispositivo) que expone el centro de IoT.
  * [Enviar mensajes del dispositivo a la nube tooIoT concentrador][devguide-messages-d2c].
  * [Leer los mensajes de dispositivo para la nube de punto de conexión integrados de hello][devguide-builtin].
  * [Uso de puntos de conexión y reglas de enrutamiento personalizados para mensajes de dispositivos a la nube][devguide-custom].
  * [Envío de mensajes de nube a dispositivo desde IoT Hub][devguide-messages-c2d].
  * [Creación y lectura de mensajes de IoT Hub][devguide-format].
* En [Carga de archivos desde un dispositivo][devguide-upload] se describe cómo se cargan archivos desde un dispositivo. artículo de Hello también incluye información acerca de temas como Hola puede enviar el proceso de carga de notificaciones Hola.
* En [Administrar identidades del dispositivo en IoT Hub][devguide-identities] se describe qué información almacena el registro de identidad de cada centro de IoT y cómo se accede a él y se modifica.
* [Controlar el acceso tooIoT concentrador] [ devguide-security] describen Hola seguridad modelo utilizado toogrant tooIoT concentrador funciones del acceso para dispositivos y componentes de la nube. Hola artículo incluye información acerca del uso de tokens y los certificados X.509 y los detalles de permisos de hello que puede conceder.
* [Usar configuraciones y estado del dispositivo: los gemelos toosynchronize] [ devguide-device-twins] describe hello *gemelas dispositivo* hello y concepto funcionalidad expone como la sincronización de un dispositivo con su dispositivo gemelas. Hola artículo incluye información sobre los datos de hello almacenados en un doble de dispositivo.
* [Invocar un método directo en un dispositivo] [ devguide-directmethods] describe Hola ciclo de vida de un método directo, obtener información acerca de cómo tooinvoke métodos en un dispositivo desde el Hola back-end de aplicación y el identificador de método directo en el dispositivo.
* En [Programación de trabajos en varios dispositivos][devguide-jobs] se describe cómo se programan trabajos en varios dispositivos. Hello artículo describe cómo toosubmit trabajos que realizar tareas como ejecutar un método directo, actualizar un dispositivo mediante un doble de dispositivo. También describe cómo tooquery Hola estado de un trabajo.
* [Referencia: elegir un protocolo de comunicaciones] [ devguide-protocol] describe los protocolos de comunicación de Hola que admite el centro de IoT para la comunicación de dispositivos y listas Hola puertos que deben estar abiertos.
* [Referencia: los extremos del centro de IoT] [ devguide-endpoints] describe Hola varios extremos que expone cada centro de IoT para las operaciones en tiempo de ejecución y administración. Hola también se describe cómo puede crear extremos adicionales en el centro de IoT y cómo toouse una conectividad de dispositivos de campo puerta de enlace tooenable tooyour centro de IoT los extremos en escenarios no estándares.
* [Referencia: lenguaje de consulta de centro de IoT para: los gemelos de dispositivo, los trabajos y el enrutamiento de mensajes] [ devguide-query] describe ese lenguaje de consulta de centro de IoT que le permite tooretrieve información desde el centro de: los gemelos de dispositivo y trabajos.
* [Referencia: las cuotas y la limitación] [ devguide-quotas] se resumen las cuotas de hello establecidas en servicio de centro de IoT de Hola y Hola comportamiento puede esperar toosee al superar una cuota de limitación.
* [Hacer referencia a-precios] [ devguide-pricing] proporciona información general sobre los diferentes SKU y los precios de centro de IoT y obtener más información sobre cómo los mensajes de Hola funcionalidades centro de IoT se miden como IoT hub.
* [Referencia: dispositivo y el servicio SDK] [ devguide-sdks] listas Hola SDK de IoT de Azure puede usar toodevelop aplicaciones de dispositivos y servicios que interactúan con el centro de IoT. artículo de Hello incluye documentación de API tooonline de vínculos.
* [Referencia: compatibilidad con IoT Hub MQTT] [ devguide-mqtt] proporciona información detallada sobre cómo centro de IoT es compatible con el protocolo MQTT Hola. artículo de Hello describe la compatibilidad con Hola Hola MQTT protocolo integrado toohello SDK de IoT de Azure y proporciona información acerca de cómo utilizar el protocolo de hello MQTT directamente.
* [Glosario][devguide-glossary], una lista de términos habituales relacionados con IoT Hub.

[devguide-messaging]: iot-hub-devguide-messaging.md
[devguide-upload]: iot-hub-devguide-file-upload.md
[devguide-identities]: iot-hub-devguide-identity-registry.md
[devguide-security]: iot-hub-devguide-security.md
[devguide-device-twins]: iot-hub-devguide-device-twins.md
[devguide-directmethods]: iot-hub-devguide-direct-methods.md
[devguide-jobs]: iot-hub-devguide-jobs.md
[devguide-endpoints]: iot-hub-devguide-endpoints.md
[devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[devguide-query]: iot-hub-devguide-query-language.md
[devguide-sdks]: iot-hub-devguide-sdks.md
[devguide-mqtt]: iot-hub-mqtt-support.md
[devguide-glossary]: iot-hub-devguide-glossary.md
[devguide-pricing]: iot-hub-devguide-pricing.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[devguide-messages-d2c]: iot-hub-devguide-messages-d2c.md
[devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[devguide-custom]: iot-hub-devguide-messages-read-custom.md
[devguide-messages-c2d]: iot-hub-devguide-messages-c2d.md
[devguide-format]: iot-hub-devguide-messages-construct.md
[devguide-protocol]: iot-hub-devguide-protocols.md
