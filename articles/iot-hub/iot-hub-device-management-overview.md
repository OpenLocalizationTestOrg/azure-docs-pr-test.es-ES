---
title: "administración de aaaDevice con el centro de IoT de Azure | Documentos de Microsoft"
description: "Información general sobre la administración de dispositivos con IoT Hub de Azure: ciclo de vida del dispositivo empresarial y patrones de administración de dispositivos como, reinicio, restablecimiento de fábrica, actualización de firmware, configuración, dispositivos gemelos, consultas y trabajos."
services: iot-hub
documentationcenter: 
author: bzurcher
manager: timlt
editor: 
ms.assetid: a367e715-55f6-4593-bd68-7863cbf0eb81
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: briz
ms.openlocfilehash: 7e22fb6eb3c541a513b16a047c7c3ef557255532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-device-management-with-iot-hub"></a>Información general sobre la administración de dispositivos con IoT Hub
## <a name="introduction"></a>Introducción
Centro de IoT de Azure proporciona características de Hola y un modelo de extensibilidad que permiten soluciones de administración de dispositivos sólida de desarrolladores back-end toobuild y dispositivo. Intervalo de dispositivos de sensores restringidos y Microcontroladores de propósito único, las puertas de enlace de toopowerful que enrutan las comunicaciones para grupos de dispositivos.  Además, los casos de uso de Hola y los requisitos para los operadores de IoT varían significativamente entre empresas.  A pesar de esta variación, administración de dispositivos con el centro de IoT proporciona capacidades de hello, los patrones y código bibliotecas toocater tooa conjunto diverso de dispositivos y usuarios finales.

Una parte fundamental de creación de una solución de IoT empresarial satisfactorio es tooprovide una estrategia para la forma en que los operadores controlan la administración continua de su colección de dispositivos de Hola. Operadores de IoT requieren herramientas confiables y simples y aplicaciones que les toofocus en hello permiten más aspectos estratégicos de sus trabajos. Este artículo ofrece:

* Una breve descripción de la administración de toodevice del enfoque de centro de IoT de Azure.
* Descripción de los principios de administración de dispositivos comunes.
* Descripción del ciclo de vida de hello dispositivos.
* Información general sobre los patrones comunes de administración de dispositivos.

## <a name="device-management-principles"></a>Principios de la administración de dispositivos
IoT incorpora un conjunto único de desafíos de administración de dispositivos y deben cumplir con todas las soluciones empresariales Hola siguientes principios:

![Gráfico de los principios de la administración de dispositivos][img-dm_principles]

* **Escala y automatización**: soluciones de IoT requieren herramientas sencillas que pueden automatizar tareas rutinarias y habilitar las operaciones relativamente pequeño personal toomanage millones de dispositivos. Diarias, operadores esperan toohandle operaciones de dispositivo de forma remota, de forma masiva y tooonly recibir alertas cuando surgen problemas que requieren su atención directa.
* **Versatilidad y compatibilidad**: ecosistema de dispositivos de hello es extraordinariamente diversos. Herramientas de administración deben estar tooaccommodate adaptar un gran número de clases de dispositivos, plataformas y protocolos. Deben ser capaz de operadores toosupport muchos tipos de dispositivos de hello más limitados embedded chips de proceso único, toopowerful y equipos totalmente funcionales.
* **Reconocimiento del contexto**: los entornos de IoT son dinámicos y cambiantes. La confiabilidad del servicio es primordial. Las operaciones de administración de dispositivos deben tener en hello cuenta después de factores tooensure ese mantenimiento tiempo de inactividad no afectan a las operaciones críticas del negocio o crear condiciones peligrosas:
    * Ventanas de mantenimiento de Acuerdo de Nivel de Servicio
    * Estados de energía y red
    * Condiciones en uso
    * Ubicación geográfica del dispositivo
* **Muchos roles de servicio**: compatibilidad con los flujos de trabajo único de Hola y procesos de las funciones de operaciones de IoT es fundamental. personal de operaciones de Hello debe funcionar armonía con hello dada las restricciones de los departamentos de TI internos.  También debe buscar formas sostenible toosurface en tiempo real dispositivo operaciones información toosupervisors y otras funciones de administración de negocio.

## <a name="device-lifecycle"></a>Ciclo de vida de dispositivo
Hay un conjunto de fases de la administración de dispositivos generales que son comunes tooall enterprise IoT proyectos. En IoT de Azure, hay cinco fases dentro del ciclo de vida del dispositivo de hello:

![Hola cinco fases del ciclo de vida de dispositivos de IoT de Azure: planear, aprovisionar, configurar, supervisar, retirar][img-device_lifecycle]

En cada una de estas cinco fases, hay varios requisitos de operador de dispositivo que deben ser entrega tooprovide una solución completa:

* **Planear**: habilitar operadores toocreate un esquema de metadatos de dispositivo que les permita tooeasily y con precisión la consulta para y dirigidos a un grupo de dispositivos para las operaciones de administración de forma masiva. Puede usar Hola dispositivo gemelas toostore estos metadatos de dispositivo en forma de Hola de etiquetas y propiedades.
  
    *Información adicional*: [empezar a trabajar con: los gemelos de dispositivo][lnk-twins-getstarted], [comprender: los gemelos de dispositivo][lnk-twins-devguide], [cómo propiedades de los dispositivos gemelas toouse][lnk-twin-properties].
* **Aprovisionar**: segura aprovisionar nuevos dispositivos tooIoT concentrador y habilitar operadores tooimmediately detectar las capacidades del dispositivo.  Usar identidades de hello centro de IoT identidad del registro toocreate dispositivo flexible y las credenciales y realizar esta operación de forma masiva mediante un trabajo. Crear dispositivos tooreport sus capacidades y condiciones mediante las propiedades de dispositivo en gemelas de dispositivo de Hola.
  
    *Información adicional*: [administrar identidades de dispositivos][lnk-identity-registry], [administración de identidades de dispositivos de forma masiva][lnk-bulk-identity], [Cómo toouse dispositivo dos propiedades][lnk-twin-properties].
* **Configurar**: facilitar masiva cambios de configuración y firmware actualiza toodevices mientras se mantiene el estado y la seguridad. Realice estas operaciones de administración de dispositivos de forma masiva usando las propiedades que desee o con métodos directos y trabajos de difusión.
  
    *Información adicional*: [usar métodos directos][lnk-c2d-methods], [invocar un método directo en un dispositivo][lnk-methods-devguide], [cómo propiedades de los dispositivos gemelas toouse][lnk-twin-properties], [programación y los trabajos de difusión][lnk-jobs], [programar trabajos en varios dispositivos] [lnk-jobs-devguide].
* **Monitor**: supervisar el estado de la colección de general del dispositivo, el estado de Hola de las operaciones en curso y tooissues avisa a los operadores que pueden requerir su atención.  Aplicar Hola dispositivo gemelas tooallow dispositivos tooreport en tiempo real las condiciones de funcionamiento y el estado de las operaciones de actualización. Generar informes de potente panel que emite más inmediato Hola expuesta mediante consultas de gemelas de dispositivo.
  
    *Información adicional*: [cómo toouse dispositivo dos propiedades][lnk-twin-properties], [lenguaje de consulta de centro de IoT para: los gemelos de dispositivo, los trabajos y el enrutamiento de mensajes] [ lnk-query-language].
* **Retirar**: reemplazar o retirar dispositivos después de un error, actualice el ciclo, o al final de Hola de duración del servicio Hola.  Usar la información de dispositivo de hello dispositivo gemelas toomaintain si el dispositivo físico de Hola se va a reemplazar o archivado si va a retirar. Hola de uso del registro de la identidad de centro de IoT para la revocación de forma segura las credenciales e identidades de dispositivo.
  
    *Información adicional*: [cómo toouse dispositivo dos propiedades][lnk-twin-properties], [administrar identidades de dispositivos][lnk-identity-registry].

## <a name="device-management-patterns"></a>Patrones de administración de dispositivos
Centro de IoT permite Hola siguiendo el conjunto de patrones de la administración de dispositivos.  Hola [tutoriales de administración de dispositivos] [ lnk-get-started] muestra con más detalle cómo tooextend estos toofit patrones su escenario exacto y cómo toodesign nuevos patrones basándose en estos principales de plantillas.

* **Reiniciar** -aplicación de back-end de hello informa a dispositivo Hola a través de un método directo que ha iniciado un reinicio.  Hola dispositivo usa Hola informado del estado de reinicio de propiedades tooupdate hello de dispositivo de Hola.
  
    ![Gráfico de los patrones de reinicio de la administración de dispositivos][img-reboot_pattern]
* **Restablecimiento de fábrica** -aplicación de back-end de hello informa a dispositivo de Hola a través de un método directo que inició un restablecimiento de fábrica.  Hola dispositivo usa Hola informó de estado de dispositivo de Hola de restablecimiento de fábrica de Hola de tooupdate de propiedades.
  
    ![Gráfico de los patrones de restablecimiento de fábrica de la administración de dispositivos][img-facreset_pattern]
* **Configuración** -aplicaciones back-end de hello usa el software de tooconfigure de propiedades de hello deseado ejecutando en el dispositivo de Hola.  Hola dispositivo usa Hola informado del estado de configuración de tooupdate de propiedades de dispositivo de Hola.
  
    ![Gráfico de los patrones de configuración de la administración de dispositivos][img-config_pattern]
* **Actualización de firmware** -aplicación de back-end de hello informa a dispositivo Hola a través de un método directo que ha iniciado una actualización de firmware.  dispositivo Hola inicia una imagen de firmware de proceso de varios pasos toodownload Hola, aplicar imagen de firmware de hello y, por último, volver a conectar toohello servicio del centro de IoT.  A lo largo del proceso de varios pasos de hello, Hola dispositivo usa Hola notificado progreso de Hola de tooupdate de propiedades y el estado del dispositivo de Hola.
  
    ![Gráfico del patrón de actualización del firmware de la administración de dispositivos][img-fwupdate_pattern]
* **Informes de progreso y el estado** -Hola solución back-end ejecuta consultas de gemelas del dispositivo, a través de un conjunto de dispositivos, tooreport en estado de Hola y el progreso de las acciones que se ejecutan en dispositivos de Hola.
  
    ![Gráfico del patrón del estado y progreso de la administración de dispositivos][img-report_progress_pattern]

## <a name="next-steps"></a>Pasos siguientes
capacidades de Hello, los patrones y las bibliotecas de código que proporciona el centro de IoT para la administración de dispositivos, le permiten aplicaciones de IoT toocreate que cumplen los requisitos de operador de enterprise IoT dentro de cada fase del ciclo de vida de dispositivo.

toocontinue obtener información sobre características de administración de dispositivos de hello en el centro de IoT, vea hello [empezar a trabajar con la administración de dispositivos] [ lnk-get-started] tutorial.

<!-- Images and links -->
[img-dm_principles]: media/iot-hub-device-management-overview/image4.png
[img-device_lifecycle]: media/iot-hub-device-management-overview/image5.png
[img-config_pattern]: media/iot-hub-device-management-overview/configuration-pattern.png
[img-facreset_pattern]: media/iot-hub-device-management-overview/facreset-pattern.png
[img-fwupdate_pattern]: media/iot-hub-device-management-overview/fwupdate-pattern.png
[img-reboot_pattern]: media/iot-hub-device-management-overview/reboot-pattern.png
[img-report_progress_pattern]: media/iot-hub-device-management-overview/report-progress-pattern.png

[lnk-twins-devguide]: iot-hub-devguide-device-twins.md
[lnk-get-started]: iot-hub-node-node-device-management-get-started.md
[lnk-twins-getstarted]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-hub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-query-language]: iot-hub-devguide-query-language.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-methods-devguide]: iot-hub-devguide-direct-methods.md
[lnk-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-jobs-devguide]: iot-hub-devguide-jobs.md
