---
title: "las cuotas de aaaUnderstand centro de IoT de Azure y la limitación | Documentos de Microsoft"
description: "Guía del desarrollador: descripción de las cuotas de Hola que aplicar hello y tooIoT concentrador espera comportamiento de limitación."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 425e1b08-8789-4377-85f7-c13131fae4ce
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 023fa29bfbfb1de35708d6d121a1c56b50adfed9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-quotas-and-throttling"></a>Referencia: Cuotas y limitación de IoT Hub

## <a name="quotas-and-throttling"></a>Cuotas y limitación
Cada suscripción de Azure puede tener como máximo 10 centros de IoT y al menos un centro gratuito.

Cada centro de IoT se aprovisiona con un determinado número de unidades en una SKU específica (para más información, consulte [Precios de Azure IoT Hub][lnk-pricing]). Hello SKU y el número de unidades determinan Hola máximo diario cuota de mensajes que puede enviar.

Hola SKU también determina Hola límites que exige el centro de IoT en todas las operaciones de limitación.

## <a name="operation-throttles"></a>Limitaciones de operación
Aceleradores de operación se muestran las limitaciones de velocidad que se aplican en intervalos de minutos de Hola y son pensado tooavoid abuso. Centro de IoT intenta tooavoid devolver errores siempre que sea posible, pero se inicia devolver las excepciones si se infringe la limitación de Hola durante demasiado tiempo.

Hola siguiente tabla muestra hello aplica aceleradores. Valores refieren tooan individuales concentrador.

| Limitación | Gratuitos y centros S1 | Centros S2 | Centros S3 | 
| -------- | ------- | ------- | ------- |
| Operaciones de registro de identidad (crear, recuperar, enumerar, actualizar y eliminar) | 1,67/s/unidad (100/min/unidad) | 1,67/s/unidad (100/min/unidad) | 83,33/s/unidad (5000/min/unidad) |
| Conexiones de dispositivos | Máximo de 100/s o 12/s/unidad <br/> Por ejemplo, dos unidades S1 equivalen a 2\*12 = 24/s, pero tendrá al menos 100/s en todas las unidades. Con nueve unidades S1 tiene 108/s (9\*12) en las unidades. | 120/s/unidad | 6000/s/unidad |
| Envíos de dispositivo a nube | Máximo de 100/s o 12/s/unidad <br/> Por ejemplo, dos unidades S1 equivalen a 2\*12 = 24/s, pero tendrá al menos 100/s en todas las unidades. Con nueve unidades S1 tiene 108/s (9\*12) en las unidades. | 120/s/unidad | 6000/s/unidad |
| Envíos de nube a dispositivo | 1,67/s/unidad (100/min/unidad) | 1,67/s/unidad (100/min/unidad) | 83,33/s/unidad (5000/min/unidad) |
| Recepciones de nube a dispositivo <br/> (solo cuando el dispositivo usa HTTP)| 16,67/s/unidad (1000/min/unidad) | 16,67/s/unidad (1000/min/unidad) | 833,33/s/unidad (50000/min/unidad) |
| Carga de archivos | 1,67 notificaciones de cargas de archivos/s/unidad (100/min/unidad) | 1,67 notificaciones de cargas de archivos/s/unidad (100/min/unidad) | 83,33 notificaciones de cargas de archivos/s/unidad (5000/min/unidad) |
| Métodos directos | 20/s/unidad | 60/s/unidad | 3000/s/unidad | 
| Lecturas de dispositivos gemelos | 10/s | Máximo de 10/s o 1/s/unidad | 50/s/unidad |
| Actualizaciones de dispositivos gemelos | 10/s | Máximo de 10/s o 1/s/unidad | 50/s/unidad |
| Operaciones de trabajos <br/> (crear, actualizar, enumerar, eliminar) | 1,67/s/unidad (100/min/unidad) | 1,67/s/unidad (100/min/unidad) | 83,33/s/unidad (5000/min/unidad) |
| Resultado de operaciones por dispositivo de trabajos | 10/s | Máximo de 10/s o 1/s/unidad | 50/s/unidad |

Es importante tooclarify que Hola *las conexiones con dispositivos* acelerador rige la tasa de hello en el que se pueden establecer nuevas conexiones de dispositivo con un centro de IoT. Hola *las conexiones con dispositivos* acelerador no controla el número máximo de Hola de dispositivos conectados al mismo tiempo. Acelerador de Hello depende en hello número de unidades que se ha aprovisionado para centro de IoT Hola.

Por ejemplo, si compra una sola unidad S1, tendrá una limitación de 100 conexiones por segundo. Por lo tanto, tooconnect 100.000 dispositivos, toma al menos 1000 segundos (aproximadamente 16 minutos). Sin embargo, puede tener el mismo número de dispositivos conectados al mismo tiempo que de dispositivos registrados en el registro de identidad.

Para una explicación más detallada del centro de IoT comportamiento de limitación vea Hola blog [centro de IoT limitación y][lnk-throttle-blog].

> [!NOTE]
> En un momento dado, es posible tooincrease cuotas o limitar límites aumentando el número de Hola de unidades de aprovisionamiento en un centro de IoT.
> 
> [!IMPORTANT]
> Las operaciones de registro de identidad están diseñadas para usarse en tiempo de ejecución en escenarios de administración y aprovisionamiento de dispositivos. La lectura o actualización de un gran número de identidades de dispositivo se realiza mediante [trabajos de importación y exportación][lnk-importexport].
> 
> 

## <a name="other-limits"></a>Otros límites

IoT Hub exige otros límites operativos:

| Operación | Límite |
| --------- | ----- |
| URI de carga de archivos | 10000 URI de SAS pueden estar fuera para una cuenta de almacenamiento al mismo tiempo. <br/> 10 URI/dispositivo de SAS puede estar fuera al mismo tiempo. |
| Trabajos | Historial de trabajos se conserva los too30 días <br/> El número máximo de trabajos simultáneos es 1 para gratuitos y S1, 5 para S2 y 10 para S3. |
| Puntos de conexión adicionales | Los centros de SKU de pago pueden tener 10 puntos de conexión adicionales. Los centros de SKU gratis pueden tener un punto de conexión adicional. |
| Reglas de enrutamiento de mensajes | Los centros de SKU de pago pueden tener 100 reglas de enrutamiento. Los centros de SKU gratis pueden tener cinco reglas de enrutamiento. |
| Mensajería de un dispositivo a la nube | Tamaño máximo del mensaje 256 KB |
| Mensajería de la nube a un dispositivo | Tamaño máximo del mensaje 64 KB |
| Mensajería de la nube a un dispositivo | El número máximo de mensajes pendientes para la entrega es 50 |

> [!NOTE]
> Hola actualmente, número máximo de dispositivos que puede conectar tooa único centro de IoT es de 500.000. Si desea tooincrease este límite, póngase en contacto con [Microsoft Support](https://azure.microsoft.com/support/options/).

## <a name="latency"></a>Latency
Centro de IoT se esfuerza por tooprovide baja latencia para todas las operaciones. Sin embargo, debido a condiciones de toonetwork y otros factores impredecibles no puede garantizar una latencia máxima. Cuando diseñe la solución, debería:

* Evitar realizar ninguna suposición acerca de la latencia máxima de Hola de cualquier operación de centro de IoT.
* Aprovisionar el centro de IoT en los dispositivos de tooyour más cercanos Hola región de Azure.
* Considere el uso de las operaciones de Azure IoT borde tooperform sensibles a la latencia en el dispositivo de Hola o en un dispositivo de puerta de enlace toohello cerrar.

Muchas unidades de IoT Hub afectan a la limitación, tal como se ha descrito anteriormente, pero no proporcionan ventajas ni garantías de latencia adicionales.
Si ve aumentos inesperados de la latencia de operación, póngase en contacto con el [Soporte técnico de Microsoft](https://azure.microsoft.com/support/options/).

## <a name="next-steps"></a>Pasos siguientes
Otros temas de referencia en la Guía del desarrollador de IoT Hub son:

* [IoT Hub endpoints][lnk-devguide-endpoints] (Puntos de conexión de IoT Hub)
* [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query] (Lenguaje de consulta de IoT Hub para dispositivos gemelos, trabajos y enrutamiento de mensajes)
* [Compatibilidad con MQTT de IoT Hub][lnk-devguide-mqtt]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-throttle-blog]: https://azure.microsoft.com/blog/iot-hub-throttling-and-you/
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
