---
title: "Glosario de centro de IoT de términos aaaAzure | Documentos de Microsoft"
description: "Guía del desarrollador - obtener un glosario de términos comunes relativos tooAzure centro de IoT."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 16ef29ea-a185-48c3-ba13-329325dc6716
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 217eb082c13e06df5c07543c65d498ad3e395939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="glossary-of-iot-hub-terms"></a>Glosario de términos de IoT Hub
Este artículo enumeran algunos de los términos comunes de hello usados en hello artículos del centro de IoT.

## <a name="advanced-message-queueing-protocol"></a>Advanced Message Queueing Protocol
[Advanced Message Queueing Protocol (AMQP)](https://www.amqp.org/) es uno de los mensajes de Hola protocolos que [centro de IoT](#iot-hub) admite para comunicarse con dispositivos. Para obtener más información acerca de hello protocolos que admite el centro de IoT de mensajería, consulte [enviar y recibir mensajes con el centro de IoT](iot-hub-devguide-messaging.md).

## <a name="azure-cli"></a>CLI de Azure
Hola [CLI de Azure](../cli-install-nodejs.md) es una herramienta multiplataforma, código abierto, basado en el shell de comandos para crear y administrar recursos de Microsoft Azure. Esta versión de CLI de Hola se implementa mediante Node.js.

## <a name="azure-cli-20"></a>CLI de Azure 2.0
Hola [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) es una herramienta multiplataforma, código abierto, basado en el shell de comandos para crear y administrar recursos de Microsoft Azure. Esta versión de vista previa de hello CLI se implementa mediante Python.


## <a name="azure-iot-device-sdks"></a>SDK de dispositivos IoT de Azure
Hay _dispositivo SDK_ disponibles para varios idiomas que le permiten toocreate [aplicaciones para dispositivos](#device-app) que interactúan con un centro de IoT. Hello centro de IoT los tutoriales muestra cómo toouse estos SDK de dispositivo. Puede encontrar código de hello y obtener más información acerca del dispositivo de hello SDK en este GitHub [repositorio](https://github.com/Azure/azure-iot-sdks).

## <a name="azure-iot-edge"></a>Azure IoT Edge
IoT borde permite que las aplicaciones de toowrite que permiten a los dispositivos conectados a la puerta de enlace toocommunicate con [centro de IoT](#iot-hub). Hello borde IoT los tutoriales muestra cómo toouse este servicio. Puede encontrar código de hello y obtener más información sobre el borde de IoT de Azure en este GitHub [repositorio](https://github.com/Azure/iot-edge).

## <a name="azure-iot-service-sdks"></a>SDK de servicios IoT de Azure
Hay _servicio SDK_ disponibles para varios idiomas que le permiten toocreate [aplicaciones back-end](#back-end-app) que interactúan con un centro de IoT. Hello centro de IoT los tutoriales muestra cómo toouse estos servicio SDK. Puede encontrar código de hello y obtener más información acerca del servicio SDK de hello en este GitHub [repositorio](https://github.com/Azure/azure-iot-sdks).

## <a name="azure-portal"></a>Azure Portal
Hola [portal de Microsoft Azure](https://portal.azure.com) es una ubicación central donde puede aprovisionar y administrar los recursos de Azure. Organiza su contenido mediante _hojas_. En algunos de los tutoriales de centro de IoT hello, se le pedirá hello toouse [portal de Azure clásico](https://manage.windowsazure.com).

## <a name="azure-powershell"></a>Azure PowerShell
[Azure PowerShell](/powershell/azure/overview) es una colección de cmdlets puede usar toomanage Azure con Windows PowerShell. Puede usar Hola cmdlets toocreate, probar, implementar y administrar soluciones y servicios que entregan a través de hello plataforma Windows Azure.

## <a name="azure-resource-manager"></a>Administrador de recursos de Azure
[El Administrador de recursos Azure](../azure-resource-manager/resource-group-overview.md) permite toowork con recursos de hello en la solución como un grupo. Puede implementar, actualizar o eliminar los recursos de Hola para su solución en una única operación coordinada.

## <a name="azure-service-bus"></a>Azure Service Bus
[Bus de servicio](../service-bus/index.md) proporciona comunicación habilitada para la nube con la mensajería empresarial y retransmitir que le ayuda a conectan soluciones locales con la nube de Hola. Algunos tutoriales de IoT Hub usan las [colas](../service-bus-messaging/service-bus-messaging-overview.md) de Service Bus.

## <a name="azure-storage"></a>Azure Storage
[Azure Storage](../storage/common/storage-introduction.md) es una solución de almacenamiento en la nube. Incluye el servicio de almacenamiento de blobs de Hola que puede usar toostore no estructurado datos del objeto. Algunos tutoriales de IoT Hub utilizan Blob Storage.

## <a name="back-end-app"></a>Aplicación de back-end
En el contexto de Hola de [centro de IoT](#iot-hub), una aplicación de back-end es una aplicación que se conecta tooone de puntos de conexión de servicio orientadas a hello en un centro de IoT. Por ejemplo, podría recuperar una aplicación back-end [dispositivo a la nube](#device-to-cloud)mensajes o administrar hello [del registro de identidad](#identity-registry). Normalmente, una aplicación back-end se ejecuta en la nube de hello, pero en muchos de los tutoriales de Hola Hola back-end aplicaciones son aplicaciones de consola que se ejecutan en el equipo de desarrollo local.

## <a name="built-in-endpoints"></a>Puntos de conexión integrados
Todas las instancias de IoT Hub incluyen un [punto de conexión](iot-hub-devguide-endpoints.md) integrado que es compatible con Event Hubs. Puede utilizar cualquier mecanismo que funciona con mensajes de dispositivo a la nube de los centros de eventos tooread desde este punto de conexión.

## <a name="cloud-gateway"></a>Puerta de enlace en la nube
Una puerta de enlace de nube habilita la conectividad para dispositivos que no se puede conectar directamente demasiado[centro de IoT](#iot-hub). Una puerta de enlace de nube está hospedada en nube de hello en contraste tooa [puerta de enlace de campo](#field-gateway) que ejecuta dispositivos tooyour local. Un caso de uso típico para una puerta de enlace de nube es tooimplement traducción de protocolos para sus dispositivos.

## <a name="cloud-to-device"></a>De la nube al dispositivo
Se refiere toomessages enviados desde un dispositivo conectado de IoT hub tooa. A menudo, estos mensajes son comandos que indique a Hola dispositivo tootake una acción. Para más información, vea [Enviar y recibir mensajes con IoT Hub](iot-hub-devguide-messaging.md).

## <a name="connection-string"></a>Cadena de conexión
Utilice las cadenas de conexión en su aplicación código tooencapsulate Hola información necesaria tooconnect tooan punto de conexión. Una cadena de conexión suele incluir dirección Hola de punto de conexión de Hola y obtener información de seguridad, pero formatos varían entre los servicios de cadena de conexión. Hay dos tipos de cadena de conexión asociada con el servicio de centro de IoT hello:
- *Las cadenas de conexión de dispositivo* habilitar dispositivos tooconnect toohello dispositivo extremos en un centro de IoT.
- *Las cadenas de conexión de centro de IoT* Habilitar puntos de conexión de aplicaciones back-end tooconnect toohello a nivel de servicio en un centro de IoT.

## <a name="custom-endpoints"></a>Puntos de conexión personalizados
Puede crear personalizado [extremos](iot-hub-devguide-endpoints.md) en un toodeliver del centro de IoT envían los mensajes por un [regla de enrutamiento](#routing-rules). Extremos personalizados conectan directamente tooan concentrador de eventos, una cola de Bus de servicio o un tema de Bus de servicio.

## <a name="custom-gateway"></a>Puerta de enlace personalizada
Una puerta de enlace habilita la conectividad para dispositivos que no se puede conectar directamente demasiado[centro de IoT](#iot-hub). Puede usar [Azure IoT borde](#azure-iot-edge) toobuild puertas de enlace personalizados que implementan los mensajes de toohandle de lógica personalizada, conversiones de protocolo personalizado y otras tareas de procesamiento en hello borde.

## <a name="data-point-message"></a>Mensaje de punto de datos
Un mensaje de punto de datos es un mensaje [del dispositivo a la nube](#device-to-cloud) que contiene datos de [telemetría](#telemetry), como la velocidad del viento o la temperatura.

## <a name="desired-configuration"></a>Configuración deseada
En el contexto de Hola de un [gemelas dispositivo](iot-hub-devguide-device-twins.md), deseado configuración hace referencia toohello conjunto completo de propiedades y metadatos de gemelas de dispositivo de Hola que se deben sincronizar con el dispositivo de Hola.

## <a name="desired-properties"></a>Propiedades deseadas
En contexto de Hola de un [gemelas dispositivo](iot-hub-devguide-device-twins.md), deseado propiedades es una subsección de gemelas de dispositivo de Hola que se usan con [notificado propiedades](#reported-properties) toosynchronize configuración del dispositivo o la condición. Propiedades deseadas solo se pueden establecer un [aplicaciones back-end](#back-end-app) y observado por hello [aplicación de dispositivo](#device-app).

## <a name="device-to-cloud"></a>Del dispositivo a la nube
Hace referencia toomessages enviados desde un dispositivo conectado demasiado[centro de IoT](#iot-hub). Estos mensajes pueden ser [puntos de datos](#data-point-message) o [mensajes](#interactive-message) interactivos. Para más información, vea [Enviar y recibir mensajes con IoT Hub](iot-hub-devguide-messaging.md).

## <a name="device"></a>Dispositivo
En el contexto de Hola de IoT, un dispositivo suele ser un dispositivo de computación independiente a pequeña escala, que puede recopilar datos o controlar otros dispositivos. Por ejemplo, un dispositivo puede ser un dispositivo de supervisión ambiental o un controlador para los sistemas de ventilación y regar hello en un efecto invernadero. Hola [catálogo dispositivo](https://catalog.azureiotsuite.com/) proporciona una lista de certificados toowork de dispositivos de hardware con [centro de IoT](#iot-hub).

## <a name="device-app"></a>Aplicación para dispositivo
Una aplicación de dispositivo se ejecuta en su [dispositivo](#device) e identificadores Hola comunicación con su [centro de IoT](#iot-hub). Normalmente, se usa uno de hello [dispositivos de IoT de Azure SDK](#azure-iot-device-sdks) cuando se implementa una aplicación de dispositivo. En muchos de los tutoriales de IoT hello, use un [dispositivo simulado](#simulated-device) para su comodidad.

## <a name="device-condition"></a>Condición de dispositivo
Hace referencia a información de estado de toodevice, como método de conectividad de hello actualmente en uso, devuelto por una [aplicación de dispositivo](#device-app). Las [aplicaciones para dispositivo](#device-app) también pueden notificar sus funcionalidades. Se puede consultar la información de condición y funcionalidad mediante dispositivos gemelos.

## <a name="device-data"></a>Datos del dispositivo
Los datos del dispositivo hace referencia a los datos de cada dispositivo de toohello almacenados en hello centro de IoT [del registro de identidad](#identity-registry). Es posible tooimport y exporte los datos.

## <a name="device-explorer"></a>Explorador de dispositivos
Hola [explorer dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) es una herramienta que se ejecuta en Windows y permite toomanage los dispositivos en hello [del registro de identidad](#identity-registry).hello herramienta también puede enviar y recibir los dispositivos de tooyour de mensajes.

## <a name="device-identities-rest-api"></a>API de REST de identidades de dispositivos
Hola [API de REST de identidades de dispositivo](https://docs.microsoft.com/rest/api/iothub/iothubresource) permite toomanage los dispositivos registrados en hello [del registro de identidad](#identity-registry) mediante una API de REST. Normalmente, debe utilizar uno de un nivel más alto de hello [servicio SDK](#azure-iot-service-sdks) tal como se muestra en hello tutoriales de centro de IoT.

## <a name="device-identity"></a>Identidad del dispositivo
identidad del dispositivo Hello es Hola identificador único asignado tooevery dispositivo registrado en hello [del registro de identidad](#identity-registry).

## <a name="device-management"></a>Administración de dispositivos
Administración de dispositivos abarca Hola ciclo de vida completo asociado a la administración de dispositivos de hello en la solución de IoT incluidas planeación, aprovisionar, configurar, supervisar y retirar.

## <a name="device-management-patterns"></a>Patrones de administración de dispositivos
[IoT Hub](#iot-hub) permite patrones comunes de administración de dispositivos incluidos el reinicio, el restablecimiento de fábrica y las actualizaciones de firmware de los dispositivos.

## <a name="device-messaging-rest-api"></a>API de REST de Device Messaging
Puede usar hello [API de REST de mensajería de dispositivo](https://docs.microsoft.com/rest/api/iothub/httpruntime) desde un dispositivo mensajes centro de IoT tooan toosend dispositivo a la nube y recibir [en la nube al dispositivo](#cloud-to-device) mensajes de un centro de IoT. Normalmente, debe utilizar uno de un nivel más alto de hello [dispositivo SDK](#azure-iot-device-sdks) tal como se muestra en hello tutoriales de centro de IoT.

## <a name="device-provisioning"></a>Aprovisionamiento de dispositivos
Aprovisionamiento de dispositivos es el proceso de Hola de agrega Hola inicial [los datos del dispositivo](#device-data) toohello se almacena en la solución. tooenable un nuevo centro de tooyour tooconnect de dispositivo, debe agregar un dispositivo Id. y claves toohello centro de IoT [del registro de identidad](#identity-registry). Como parte del proceso de aprovisionamiento de hello, podría necesitar datos específicos del dispositivo de tooinitialize en otros almacenes de solución.

## <a name="device-twin"></a>Dispositivo gemelo
Un [dispositivo gemelo](iot-hub-devguide-device-twins.md) es un documento JSON que almacena información sobre el estado de los dispositivos, como metadatos, configuraciones y condiciones. [IoT Hub](#iot-hub) conserva un dispositivo gemelo por cada dispositivo que se aprovisiona en el centro de IoT. : Los gemelos de dispositivo permiten toosynchronize [condiciones de dispositivo](#device-condition) y las configuraciones entre dispositivos de Hola y solución de hello back-end. Puede consultar dispositivos específicos de dispositivo: los gemelos toolocate y consultar el estado de Hola de operaciones de larga duración.

## <a name="device-twin-queries"></a>Consultas de dispositivos gemelos
[Las consultas de dispositivo gemelas](iot-hub-devguide-query-language.md) use Hola centro de IoT similar a SQL consulta lenguaje tooretrieve información desde sus: los gemelos de dispositivo. Puede usar Hola mismo centro de IoT consultar información del idioma de tooretrieve sobre [trabajos](#job) ejecutando en el centro de IoT.

## <a name="device-twin-rest-api"></a>API de REST de dispositivos gemelos
Puede usar hello [API de REST de dispositivo gemelas](https://docs.microsoft.com/rest/api/iothub/devicetwinapi) de solución de hello back end toomanage: los gemelos de su dispositivo. Hola API permite tooretrieve y update [gemelas dispositivo](#device-twin) propiedades e invocar [dirigir métodos](#direct-method). Normalmente, debe utilizar uno de un nivel más alto de hello [servicio SDK](#azure-iot-service-sdks) tal como se muestra en hello tutoriales de centro de IoT.

## <a name="device-twin-synchronization"></a>Sincronización de dispositivos gemelos
Sincronización de dispositivos gemelas usa hello [deseado propiedades](#desired-properties) en su tooconfigure: los gemelos de dispositivo los dispositivos y recuperar [notificado propiedades](#reported-properties) desde su toostore de dispositivos en gemelas de dispositivo de Hola.

## <a name="direct-method"></a>Método directo
A [método directo](iot-hub-devguide-direct-methods.md) es una manera para tootrigger un tooexecute de método en un dispositivo mediante la invocación de una API en su centro de IoT.

## <a name="endpoint"></a>Extremo
Un centro de IoT expone varios [extremos](iot-hub-devguide-endpoints.md) que permiten su centro de IoT de aplicaciones tooconnect toohello. No hay puntos de conexión de dispositivo que permiten operaciones de tooperform dispositivos tales como el envío [dispositivo a la nube](#device-to-cloud) mensajes y la recepción [en la nube al dispositivo](#cloud-to-device) mensajes. Hay extremos de administración a nivel de servicio que permiten [aplicaciones back-end](#back-end-app) tooperform operaciones como [identidad del dispositivo](#device-identity) administración y administración de dispositivos gemelas. Hay [puntos de conexión integrados](#built-in-endpoints) orientados al servicio para leer mensajes del dispositivo a la nube. Puede crear [extremos personalizados](#custom-endpoints) tooreceive mensajes de dispositivo para la nube enviados un [regla de enrutamiento](#routing-rules).

## <a name="event-hubs-service"></a>Servicio Event Hubs
[Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) es un servicio de entrada de datos altamente escalable que puede ingerir millones de eventos por segundo. servicio de Hello permite tooprocess y analizar Hola grandes cantidades de datos generados por los dispositivos conectados y las aplicaciones. Para obtener una comparación con el servicio de centro de IoT hello, consulte [comparación al centro de IoT de Azure y concentradores de eventos de Azure](iot-hub-compare-event-hubs.md).

## <a name="event-hub-compatible-endpoint"></a>Punto de conexión compatible con Event Hub
tooread [dispositivo a la nube](#device-to-cloud) centro de IoT tooyour envían los mensajes, puede conectar el extremo de tooan en el centro y usar cualquier tooread de método de concentrador de eventos-compatible con esos mensajes. Los métodos compatibles con el concentrador de eventos incluyen el uso de hello [SDK de los centros de eventos](../event-hubs/event-hubs-programming-guide.md) y [análisis de transmisiones de Azure](../stream-analytics/stream-analytics-introduction.md).

## <a name="field-gateway"></a>Puerta de enlace de campo
Una puerta de enlace de campo habilita la conectividad para dispositivos que no se puede conectar directamente demasiado[centro de IoT](#iot-hub) y normalmente se implementa localmente con los dispositivos. Para más información, consulte [¿Qué es Azure IoT Hub?](iot-hub-what-is-iot-hub.md)

## <a name="free-account"></a>Cuenta gratuita
Puede crear un [libre cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/) toocomplete Hola tutoriales de centro de IoT y experimentar con el servicio del centro de IoT hello (y otros servicios de Azure).

## <a name="gateway"></a>Puerta de enlace
Una puerta de enlace habilita la conectividad para dispositivos que no se puede conectar directamente demasiado[centro de IoT](#iot-hub). Consulte también [Puerta de enlace de campo](#field-gateway), [Puerta de enlace en la nube](#cloud-gateway) y [Puerta de enlace personalizada](#custom-gateway).

## <a name="identity-registry"></a>Registro de identidad
Hola [del registro de identidad](iot-hub-devguide-identity-registry.md) será componente integrado de Hola de un centro de IoT que almacena información sobre dispositivos individuales Hola permita tooconnect tooan IoT hub.

## <a name="interactive-message"></a>Mensaje interactivo
Un mensaje interactivo es un [en la nube al dispositivo](#cloud-to-device) mensaje que desencadena una acción inmediata en hello solución back-end. Por ejemplo, un dispositivo puede enviar una alarma sobre un error que se debe registrar automáticamente en el sistema CRM tooa.

## <a name="iot-hub"></a>IoT Hub
IoT Hub es un servicio de Azure totalmente administrado que permite la comunicación bidireccional confiable y segura entre millones de dispositivos y un back-end de soluciones. Para más información, consulte [¿Qué es Azure IoT Hub?](iot-hub-what-is-iot-hub.md) Con su [suscripción de Azure](#subscription), puede crear toohandle de centros de IoT su IoT las cargas de trabajo de mensajería.

## <a name="iot-hub-metrics"></a>Métricas de IoT Hub
[Las métricas de centro de IoT](iot-hub-metrics.md) le proporciona datos sobre el estado de Hola de centros de IoT de hello en su [suscripción de Azure](#subscription). Habilitar las métricas de centro de IoT se tooassess Hola estado general del servicio de Hola y los dispositivos de hello conectado tooit. Las métricas de centro de IoT pueden ayudarle a ver lo que ocurre con el centro de IoT e investigar problemas de causa raíz sin necesidad de toocontact soporte técnico de Azure.

## <a name="iot-hub-query-language"></a>Lenguaje de consulta de IoT Hub
Hola [lenguaje de consultas del centro de IoT](iot-hub-devguide-query-language.md) es un lenguaje parecido a SQL que le permite tooquery su [trabajos](#job) y: los gemelos de dispositivo.

## <a name="iot-hub-resource-provider-rest-api"></a>API de REST del proveedor de recursos de IoT Hub
Puede usar hello [API de REST de proveedor de recursos de centro de IoT](https://docs.microsoft.com/rest/api/iothub/resourceprovider/iot-hub-resource-provider-rest) toomanage centros de IoT hello en su [suscripción de Azure](#subscription) realizando operaciones como crear, actualizar y eliminar los concentradores.

## <a name="iot-suite"></a>IoT Suite
Paquetes del Conjunto de aplicaciones de IoT de Azure con distintos servicios de Azure con soluciones preconfiguradas. Estas soluciones preconfiguradas permiten tooget a trabajar rápidamente con implementaciones de-to-end de escenarios comunes de IoT. Para más información, vea [¿Qué es el Conjunto de aplicaciones de IoT de Azure?](../iot-suite/iot-suite-overview.md)

## <a name="iothub-explorer"></a>iothub-explorer
Hola [el centro de IOT explorador](https://github.com/azure/iothub-explorer) es una herramienta de línea de comandos entre plataformas. herramienta de Hello permite toomanage los dispositivos en hello [del registro de identidad](#identity-registry), enviar y recibir mensajes y archivos de los dispositivos y supervisar las operaciones del centro de IoT.

## <a name="job"></a>Trabajo
Puede usar el back-end de soluciones [trabajos](iot-hub-devguide-jobs.md) tooschedule y realizar un seguimiento de las actividades en un conjunto de dispositivos registrados con el centro de IoT. Las actividades incluyen actualizar las [propiedades deseadas](#desired-properties) del dispositivo gemelo, actualizar las [etiquetas](#tags) del dispositivo gemelo e invocar [métodos directos](#direct-method). [Centro de IoT](#iot-hub) también utiliza trabajos demasiado[importar exportación tooand](iot-hub-devguide-identity-registry.md#import-and-export-device-identities) de hello [del registro de identidad](#identity-registry).

## <a name="jobs-rest-api"></a>API DE REST de trabajos
Hola [API de REST de trabajos](https://docs.microsoft.com/rest/api/iothub/jobapi) permite toomanage [trabajos](#job) ejecutando en el centro de IoT.

## <a name="module"></a>Módulo
En [Azure IoT Edge](iot-hub-linux-iot-edge-get-started.md), un [módulo](iot-hub-linux-iot-edge-get-started.md) es un componente que realiza una tarea específica. Pueden incluir tareas introducir un mensaje desde un dispositivo, transformar un mensaje o enviarlos a un centro de IoT tooan de mensaje. Un agente es responsable de reenviar los mensajes entre los módulos. Azure IoT Edge incluye un conjunto de módulos de ejemplo. También se pueden crear módulos propios personalizados.

## <a name="mqtt"></a>MQTT
[MQTT](http://mqtt.org/) es uno de los mensajes de Hola protocolos que [centro de IoT](#iot-hub) admite para comunicarse con dispositivos. Para obtener más información acerca de hello protocolos que admite el centro de IoT de mensajería, consulte [enviar y recibir mensajes con el centro de IoT](iot-hub-devguide-messaging.md).

## <a name="operations-monitoring"></a>Supervisión de operaciones
Centro de IoT [supervisión de operaciones](iot-hub-operations-monitoring.md) permite toomonitor Hola estado de las operaciones en el centro de IoT en tiempo real. [IoT Hub](#iot-hub) realiza el seguimiento de eventos a través de varias categorías de operaciones. Puede optar por enviar eventos de uno o más categorías tooan extremo del centro de IoT para su procesamiento. Puede supervisar los datos de Hola para errores o establecer un procesamiento más complejo basándose en patrones de datos.

## <a name="physical-device"></a>Dispositivo físico
Un dispositivo físico es un dispositivo real, como una instrucción de procesamiento de frambuesa que conecta el centro de IoT tooan. Para mayor comodidad, muchos de los tutoriales de centro de IoT Hola usan [simular dispositivos](#simulated-device) tooenable toorun los ejemplos en el equipo local.

## <a name="primary-and-secondary-keys"></a>Claves principales y secundarias
Cuando se conecta a nivel de dispositivo de tooa o punto de conexión de servicio orientado en un centro de IoT, su [cadena de conexión](#connection-string) incluye toogrant clave tiene acceso a. Cuando se agrega un dispositivo toohello [del registro de identidad](#identity-registry) o agregar un [directiva de acceso compartido](#shared-access-policy) tooyour concentrador, servicio de hello genera una clave principal y secundaria. Tener dos claves permite tooroll sobre desde una tooanother clave cuando se actualiza una clave sin perder el centro de IoT de toohello de acceso.

## <a name="protocol-gateway"></a>Puerta de enlace de protocolo
Una puerta de enlace de protocolo normalmente se implementa en la nube de Hola y proporciona servicios de traducción para dispositivos que se conectan demasiado de protocolo[centro de IoT](#iot-hub). Para más información, consulte [¿Qué es Azure IoT Hub?](iot-hub-what-is-iot-hub.md)

## <a name="quotas-and-throttling"></a>Cuotas y limitación
Hay varios [cuotas](iot-hub-devguide-quotas-throttling.md) que aplican tooyour uso de [centro de IoT](#iot-hub), muchas de hello varían las cuotas basada en nivel de hello del centro de IoT Hola. [Centro de IoT](#iot-hub) también se aplica [limita](iot-hub-devguide-quotas-throttling.md) tooyour uso del servicio de hello en tiempo de ejecución.

## <a name="reported-configuration"></a>Configuración notificada
En el contexto de Hola de un [gemelas dispositivo](iot-hub-devguide-device-twins.md), incluido configuración hace referencia toohello conjunto completo de propiedades y metadatos en gemelas de dispositivo de Hola que deben estar registrados toohello back-end de soluciones.

## <a name="reported-properties"></a>Propiedades notificadas
En el contexto de Hola de un [gemelas de dispositivo](iot-hub-devguide-device-twins.md), informó de propiedades es una subsección de hello dispositivo gemelas utilizado con [las propiedades adecuadas](#desired-properties) toosynchronize configuración del dispositivo o la condición. Notifica solo se pueden establecer propiedades hello [aplicación de dispositivo](#device-app) pueden leer y consultar un [aplicaciones back-end](#back-end-app).

## <a name="resource-group"></a>Grupos de recursos
[El Administrador de recursos Azure](#azure-resource-manager) toogroup de grupos de recursos utiliza recursos relacionados con juntos. Puede usar una operación de tooperform de grupo de recursos en todos los recursos de hello en el grupo de hello simultáneamente.

## <a name="retry-policy"></a>Directiva de reintentos
Usar un toohandle de directiva de reintento [errores transitorios](https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx) cuando se conecta el servicio de nube tooa.

## <a name="routing-rules"></a>Reglas de enrutamiento
Configurar [reglas de enrutamiento](iot-hub-devguide-messages-read-custom.md) en su tooa de mensajes del dispositivo a la nube de IoT hub tooroute [extremo predefinido](#built-in-endpoints) o demasiado[extremos personalizados](#custom-endpoints) para su procesamiento mediante la copia de seguridad de la solución final.

## <a name="sasl-plain"></a>SASL PLAIN
SASL simple es un protocolo que Hola [AMQP](#advanced-message-queue-protocol) protocolo usa tokens de seguridad de tootransfer.

## <a name="shared-access-signature"></a>Firma de acceso compartido
Las firmas de acceso compartido (SAS) son un mecanismo de autenticación basado en valores hash seguros SHA-256 o en URI. La autenticación de SAS tiene dos componentes: una _directiva de acceso compartido_ y una _firma de acceso compartido_ (a menudo denominada token). Un dispositivo usa SAS tooauthenticate con un centro de IoT. [Aplicaciones de back-end](#back-end-app) usar SAS tooauthenticate con puntos de conexión de servicio orientadas a hello en un centro de IoT. Normalmente, incluye el token de SAS de Hola Hola [cadena de conexión](#connection-string) que una aplicación usa tooestablish un centro de IoT tooan de conexión.

## <a name="shared-access-policy"></a>Directiva de acceso compartido
Una directiva de acceso compartido define permisos de hello concedidos tooanyone que tiene una válida [clave primaria o secundaria](#primary-and-secondary-keys) asociada a esa directiva. Puede administrar las directivas de acceso compartido de Hola y las claves de la base de datos central en hello [portal](#azure-portal).

## <a name="simulated-device"></a>Dispositivo simulado
Para mayor comodidad, muchas de hello centro de IoT tutoriales usa simulan tooenable dispositivos toorun los ejemplos en el equipo local. En cambio, un [dispositivo físico](#physical-device) es un dispositivo real, como una instrucción de procesamiento de frambuesa que conecta el centro de IoT tooan.

## <a name="solution"></a>Solución
A _solución_ pueden hacer referencia tooa solución de Visual Studio que incluye uno o más proyectos. A _solución_ también podría hacer referencia tooan IoT solución que incluye elementos como los dispositivos, [aplicaciones para dispositivos](#device-app), un centro de IoT, otros servicios de Azure, y [aplicaciones back-end](#back-end-app).

## <a name="subscription"></a>La suscripción
Una suscripción de Azure es donde se realiza la facturación. Cada recurso de Azure que se crea o servicio de Azure que se utiliza está asociado a una única suscripción. Muchas cuotas también se aplican en el nivel de Hola de una suscripción.

## <a name="system-properties"></a>Propiedades del sistema
En el contexto de Hola de un [gemelas dispositivo](iot-hub-devguide-device-twins.md), propiedades del sistema son de solo lectura e incluyen información sobre el uso del dispositivo hello como último estado de conexión y tiempo de actividad.

## <a name="tags"></a>Etiquetas
En el contexto de Hola de un [gemelas de dispositivo](iot-hub-devguide-device-twins.md), las etiquetas son metadatos del dispositivo almacena y recupera back-end de soluciones de hello en forma de Hola de un documento JSON. Las etiquetas no son tooapps visible en un dispositivo.

## <a name="telemetry"></a>Telemetría
Dispositivos recopilar datos de telemetría, como velocidad del viento o temperatura y use [mensajes de punto de datos](#data-point-messages) centro de IoT de toosend Hola telemetría tooan.

## <a name="token-service"></a>Servicio de token
Puede usar un mecanismo de autenticación de servicio de token tooimplement para sus dispositivos. Usa un centro de IoT [directiva de acceso compartido](#shared-access-policy) con **DeviceConnect** permisos toocreate *centrada en el dispositivo* símbolos (tokens). Estos tokens habilitar un centro de IoT de dispositivo tooconnect tooyour. Un dispositivo usa un tooauthenticate del mecanismo de autenticación personalizada con el servicio de token de Hola. Si se autentica correctamente el dispositivo hello, servicio de token de hello emite un token SAS para hello dispositivo toouse tooaccess su centro de IoT.

## <a name="x509-client-certificate"></a>Certificado de cliente X.509
Un dispositivo puede usar un tooauthenticate de certificado X.509 con [centro de IoT](#iot-hub). Mediante un certificado X.509 es una alternativa toousing una [token SAS](#shared-access-signature).
