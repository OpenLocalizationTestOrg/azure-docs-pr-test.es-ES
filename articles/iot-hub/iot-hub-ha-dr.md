---
title: "Centro de IoT alta disponibilidad y recuperación ante desastres aaaAzure | Documentos de Microsoft"
description: "Describe las características de Azure y centro de IoT de Hola que le ayudarán a toobuild soluciones de alta disponibilidad IoT de Azure con capacidades de recuperación ante desastres."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: ae320e58-aa20-45b9-abdc-fa4faae8e6dd
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: elioda
ms.openlocfilehash: 74e1fa1682258819ffb3fd84eb79e42fc6e4120f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-high-availability-and-disaster-recovery"></a>Alta disponibilidad y recuperación ante desastres del Centro de IoT
Como un servicio de Azure, centro de IoT proporciona alta disponibilidad (HA) mediante redundancias en nivel de región de Azure de hello, sin ningún trabajo adicional necesario para soluciones de Hola. plataforma de Microsoft Azure Hello también incluye toohelp características generar soluciones con capacidad de recuperación (DR) o disponibilidad entre regiones. Si desea tooprovide global, entre regiones alta disponibilidad para dispositivos o usuarios, diseñar y preparar sus soluciones tootake aprovechar estas características de recuperación ante desastres de Azure. artículo de Hello [orientación técnica de continuidad de negocio de Azure](../resiliency/resiliency-technical-guidance.md) describe características integradas de hello en Azure para la continuidad del negocio y recuperación ante desastres. Hola [recuperación ante desastres y alta disponibilidad para las aplicaciones de Azure] [ Disaster recovery and high availability for Azure applications] documento proporciona instrucciones de arquitectura sobre las estrategias para las aplicaciones de Azure tooachieve alta disponibilidad y recuperación ante desastres.

## <a name="azure-iot-hub-dr"></a>Recuperación ante desastres de Centro de IoT de Azure
Además HA región toointra, centro de IoT implementa mecanismos de conmutación por error para la recuperación ante desastres que no requieren intervención del usuario de Hola. Recuperación ante desastres de centro de IoT se inicia automáticamente y tiene un objetivo de tiempo de recuperación (RTO) de hello después de objetivos de punto de recuperación (RPO) y de 26 de 2 horas.

| Funcionalidad | RPO |
| --- | --- |
| Disponibilidad de servicio para las operaciones de registro y comunicación |Posible pérdida de CName |
| Datos de identidad en el registro de identidad |Pérdida de datos de 0-5 minutos |
| Mensajes de dispositivo a nube |Se pierden todos los mensajes no leídos |
| Mensajes de supervisión de operaciones |Se pierden todos los mensajes no leídos |
| Mensajes de nube a dispositivo |Pérdida de datos de 0-5 minutos |
| Cola de comentarios de nube a dispositivo |Se pierden todos los mensajes no leídos |

## <a name="regional-failover-with-iot-hub"></a>Conmutación por error regional con el Centro de IoT
Una descripción completa de las topologías de implementación de soluciones de IoT está fuera de ámbito Hola de este artículo. artículo de Hello describe hello *conmutación por error regional* modelo de implementación para el propósito de Hola de alta disponibilidad y recuperación ante desastres.

En un modelo de conmutación por error regional, Hola solución back-end ejecuta principalmente en la ubicación de un centro de datos y una secundaria centro de IoT y el back-end se implementan en otra ubicación de centro de datos. Si el centro de IoT Hola Hola centro de datos principal sufre una interrupción o se interrumpe la conectividad de red de Hola desde el centro de datos principal de hello dispositivo toohello. Los dispositivos utilizan un punto de conexión de servicio secundario siempre que no se puede alcanzar la puerta de enlace de hello principal. Con una capacidad entre regiones conmutación por error, puede mejorarse la disponibilidad de la solución de hello más allá de alta disponibilidad de una única región de Hola.

En un nivel alto, tooimplement un modelo de conmutación por error regional con el centro de IoT, necesita Hola siguiente:

* **Un centro de IoT y la lógica de enrutamiento del dispositivo secundaria**: en caso de hello de una interrupción del servicio en su región primaria, dispositivos deben iniciar la región secundaria de conexión tooyour. Dada la naturaleza de compatible con el estado de saludo de la mayoría de los servicios implicada, es común para el proceso de solución administradores tootrigger Hola región entre conmutación por error. Hola mejor manera toocommunicate Hola nuevo punto de conexión toodevices, sin perder el control del proceso de hello, es toohave ellos comprueban con regularidad un *supervisor* servicio de punto de conexión activo Hola actual. Hello servicio de supervisor puede ser una aplicación web que se replica y mantiene accesible mediante técnicas de redirección de DNS (por ejemplo, si se usa [Azure Traffic Manager][Azure Traffic Manager]).
* **Replicación de registro de identidad** -toobe utilizable, centro de IoT secundaria Hola debe contener todas las identidades de dispositivos que se pueden conectar toohello solución. solución de Hello debe mantener copias de seguridad de replicación geográfica de identidades de dispositivos y cargarlos toohello centro de IoT secundaria antes de cambiar un punto de conexión activo de Hola para dispositivos de Hola. función de exportación de identidad de dispositivo de Hola de centro de IoT es útil en este contexto. Para obtener más información, consulte la [guía para desarrolladores de IoT Hub sobre registro de identidad][IoT Hub developer guide - identity registry].
* **Combinación lógica** : si región principal Hola vuelva a estar disponible, todos Hola estado y datos que se han creado en el sitio secundario de hello deben región principal migrados toohello atrás. Este estado y los datos principalmente está relacionada con las identidades de toodevice y metadatos de la aplicación, que se deben combinar con el centro de IoT principal de Hola y cualquier otro almacén específica de la aplicación en la región principal de Hola. toosimplify este paso, debe usar las operaciones de idempotente. Operaciones de idempotente minimizar Hola efectos secundarios de una distribución coherente eventual Hola de eventos y de duplicados o fuera de servicio entrega de eventos. Además, debe ser lógica de la aplicación hello tootolerate diseñada posibles incoherencias o "ligeramente" estado de la fecha de. Esta situación puede producirse toohello tiempo adicional necesario para el sistema de Hola demasiado "reparación" en función de los objetivos de punto de recuperación (RPO).

## <a name="next-steps"></a>Pasos siguientes
Siga estos toolearn de vínculos más información acerca del centro de IoT de Azure:

* [Introducción a los centros de IoT (tutorial)][lnk-get-started]
* [¿Qué es Azure IoT Hub?][What is Azure IoT Hub?]

[Disaster recovery and high availability for Azure applications]: ../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md
[Azure Business Continuity Technical Guidance]: https://azure.microsoft.com/documentation/articles/resiliency-technical-guidance/
[Azure Traffic Manager]: https://azure.microsoft.com/documentation/services/traffic-manager/
[IoT Hub developer guide - identity registry]: iot-hub-devguide-identity-registry.md

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[What is Azure IoT Hub?]: iot-hub-what-is-iot-hub.md
