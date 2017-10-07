---
title: "aaaInternet cosas prácticas recomendadas de seguridad | Documentos de Microsoft"
description: "artículo de Hello proporciona una lista protegida de Microsoft Internet de las prácticas recomendadas de seguridad de elementos y las recomendaciones generales."
services: security
documentationcenter: na
author: TomShinder
manager: StevenPo
editor: TomSh
ms.assetid: 2d5598c5-4c30-481d-b8f4-51ee024ea9a7
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: yurid
ms.openlocfilehash: 7ee31c912e8ac230ffa5efcd5b4c2b0b0713584f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a>Procedimientos recomendados de seguridad de Internet de las cosas
Infraestructura de Internet de las cosas (IoT) Hola protección es una tarea crítica para todas las personas implicadas con soluciones de IoT. Debido a hello y número de Hola de dispositivos utilizados naturaleza distribuida de estos dispositivos, el impacto de hello un evento de seguridad relacionados con toocompromise de millones de dispositivos de IoT no es trivial y puede tener un impacto masivo.

Por este motivo, la seguridad de IoT necesita un enfoque de seguridad en profundidad. Datos necesidades toobe seguro en la nube de Hola y tal como se mueve a través de redes públicas y privadas. Métodos deben toobe en lugar toosecurely aprovisionar Hola IoT propios dispositivos. Cada capa de dispositivo, toonetwork, toocloud back-end debe garantías de seguridad seguro.

Prácticas recomendadas de IoT se pueden clasificar de hello siguiente forma:

* Integrador o fabricante del hardware de IoT
* Desarrollador de soluciones de IoT
* Implementador de soluciones de IoT
* Operador de soluciones de IoT

En este artículo se resumen los [Procedimientos recomendados de seguridad de Internet de las cosas](../iot-suite/iot-security-best-practices.md). Consulte el artículo toothat para obtener información más detallada.

## <a name="iot-hardware-manufacturer-or-integrator"></a>Integrador o fabricante del hardware de IoT
Si es un fabricante de hardware de IoT o un integrador de hardware, siga Hola los procedimientos recomendados siguientes:

* **Definir el ámbito de los requisitos de hardware toominimum**: diseño de hardware de hello debe incluir las características mínimas necesarias para el funcionamiento de hardware de Hola y nada más. 
* **Asegúrese de hardware a prueba de manipulaciones**: compilar en mecanismos toodetect manipulación física de hardware, como la apertura de la cubierta del dispositivo de hello, quitar un elemento de dispositivo de hello, etcetera. 
* **Basarse en hardware seguro:**si [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) lo permite, cree características de seguridad como el almacenamiento seguro y cifrado y la funcionalidad de arranque basada en el Módulo de plataforma segura (TPM).
* **Proteger las actualizaciones**: actualizar el firmware durante la duración del dispositivo de hello es inevitable.

## <a name="iot-solution-developer"></a>Desarrollador de soluciones de IoT
Si es un desarrollador de la solución de IoT, siga Hola recomendaciones siguientes:

* **Siga la metodología de desarrollo de software seguro**: desarrollo de software seguro requiere el terreno pensar sobre seguridad desde el comienzo de hello del proyecto de hello todos implementación de hello forma tooits, prueba e implementación.
* **Elija el software de código abierto con cuidado**: software de código abierto ofrece la oportunidad tooquickly desarrollar soluciones.
* **Integrar con cuidado**: existen muchos de brechas de seguridad de software de hello en límite de Hola de bibliotecas y API. 

## <a name="iot-solution-deployer"></a>Implementador de soluciones de IoT
Si eres un implementador de la solución de IoT, siga Hola recomendaciones siguientes:

* **Implementar hardware de forma segura**: implementaciones de IoT podrían requerir que toobe de hardware implementado en ubicaciones no seguras, como se muestra en los espacios públicos o configuraciones regionales supervisadas.
* **Mantener las claves de autenticación seguros**: durante la implementación, cada dispositivo requiere que los identificadores de dispositivo y asociados de claves de autenticación generadas por el servicio en la nube Hola. Mantener estas claves físicamente segura incluso después de la implementación de Hola. Puede utilizarse cualquier tecla comprometido por un dispositivo malintencionado toomasquerade como un dispositivo existente.

## <a name="iot-solution-operator"></a>Operador de soluciones de IoT
Si es un operador de solución de IoT, siga Hola recomendaciones siguientes:

* **Mantener los sistemas de toodate**: asegúrese de que todos los controladores de dispositivos y sistemas operativos de dispositivos son versiones más recientes de toohello actualizada. 
* **Proteger frente a actividades malintencionadas**: si se permite el sistema operativo de hello, coloque las características más recientes de antivirus y anti-malware hello en cada sistema operativo del dispositivo. 
* **Auditar con frecuencia**: auditoría IoT infraestructura para problemas es clave cuando responde toosecurity incidentes relacionados con la seguridad.
* **Proteger físicamente la infraestructura de IoT de Hola**: Hola peor ataques de seguridad en la infraestructura de IoT se inician mediante el acceso físico toodevices.
* **Proteger las credenciales de nube**: credenciales de autenticación de nube usadas para configurar y usar una implementación de IoT son posiblemente acceso de toogain de manera más fácil de Hola y poner en peligro un sistema de IoT. 

