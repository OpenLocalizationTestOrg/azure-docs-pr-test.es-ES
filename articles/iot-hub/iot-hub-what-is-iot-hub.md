---
title: "información general del centro de IoT aaaAzure | Documentos de Microsoft"
description: "Información general de hello servicio del centro de IoT de Azure: ¿qué es el centro de IoT, conectividad de dispositivos, internet de patrones de comunicación de cosas, las puertas de enlace y patrón de comunicación asistidas por el servicio de Hola"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0b46868a1ec9e13c8f107b90269c5307f4ba27c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-iot-hub-service"></a>Información general de hello servicio del centro de IoT de Azure

Página principal del centro de IoT tooAzure. En este artículo se proporciona información general del centro de IoT de Azure y describe por qué debería usar este tooimplement servicio una solución de Internet de las cosas (IoT). El Centro de IoT de Azure es un servicio totalmente administrado que permite la comunicación bidireccional fiable y segura entre millones de dispositivos IoT y un back-end de soluciones. Centro de IoT de Azure:

* Proporciona varias opciones de comunicación de dispositivo a la nube y de la nube al dispositivo, como métodos de solicitud y respuesta, mensajería unidireccional y transferencia de archivos.
* Proporciona mensajes declarativa integrado enrutamiento tooother servicios de Azure.
* Proporciona almacenamiento consultable para metadatos del dispositivo e información de estado sincronizada.
* Habilita las comunicaciones seguras y el control de acceso con claves de seguridad por dispositivo o certificados X.509.
* Proporciona una supervisión exhaustiva para la conectividad de dispositivos y los eventos de administración de identidad de dispositivos.
* Incluye bibliotecas de dispositivo para los lenguajes más populares de Hola y plataformas.

artículo de Hello [comparación de centro de IoT y concentradores de eventos] [ lnk-compare] hello las principales diferencias entre estos dos servicios se describe y resalta las ventajas de Hola de usar el centro de IoT en sus soluciones de IoT.

Para obtener más información sobre cómo Azure y centro de IoT ayudar a proteger la solución de IoT, consulte [seguridad de Internet de las cosas de hello masa][lnk-security-ground-up].

![Centro de IoT de Azure como solución de puerta de enlace de nube en Internet de las cosas][img-architecture]

> [!NOTE]
> Para obtener una explicación más detallada de la arquitectura de IoT, vea hello [arquitectura de referencia de Microsoft Azure IoT][lnk-refarch].

## <a name="iot-device-connectivity-challenges"></a>Problemas de conectividad de dispositivos IoT

Centro de IoT y Hola bibliotecas de dispositivo le ayudarán a desafíos de hello toomeet de cómo tooreliably y conectarse de forma segura los dispositivos toohello solución back-end. Dispositivos IoT:

* A menudo son sistemas insertados sin operador humano.
* Pueden encontrarse en ubicaciones remotas, donde el acceso físico resulta costoso.
* Solo puede ser accesible a través de hello solución back-end.
* Es posible que tengan limitaciones de recursos de procesamiento y alimentación.
* Es posible que tengan conectividad de red intermitente, lenta o costosa.
* Puede necesitar toouse protocolos de aplicación propios, personalizados o específicos del sector.
* Pueden crearse mediante un amplio conjunto de plataformas populares de hardware y software.

Además toohello requisitos anteriores, cualquier solución de IoT debe también ofrecen escalabilidad, seguridad y confiabilidad. conjunto resultante de Hola de requisitos de conectividad es tooimplement de disco duro y llevar mucho tiempo cuando se usa las tecnologías tradicionales, como contenedores de web y agentes de mensajería.

## <a name="why-use-azure-iot-hub"></a>¿Por qué usar Azure IoT Hub?

Además conjunto enriquecido de tooa de [dispositivo a la nube] [ lnk-d2c-guidance] y [en la nube al dispositivo] [ lnk-c2d-guidance] opciones de comunicación, como mensajería, de archivos las transferencias y métodos de solicitud y respuesta, direcciones de centro de IoT de Azure Hola desafíos de conectividad del dispositivo en hello siguientes maneras:

* **Dispositivos gemelos**. Con los [dispositivos gemelos][lnk-twins] puede almacenar, sincronizar y consultar metadatos e información de estado de los dispositivos. Los dispositivos gemelos son documentos JSON que almacenan información sobre el estado de los dispositivos (metadatos, configuraciones y condiciones). Centro de IoT conserva a un gemelas de dispositivo para cada dispositivo que conecte tooIoT concentrador.

* **Autenticación por dispositivo y conectividad segura**. Puede aprovisionar cada dispositivo con su propio [clave de seguridad] [ lnk-devguide-security] tooenable, tooconnect tooIoT concentrador. Hola [del registro de la identidad de centro de IoT] [ lnk-devguide-identityregistry] almacena identidades de dispositivos y las claves en una solución. Un back-end de soluciones puede agregar dispositivos individuales tooallow o denegar listas tooenable un control completo sobre el acceso a los dispositivos.

* **Ruta de dispositivo a nube mensajes servicios tooAzure en función de reglas declarativas**. Centro de IoT permite toodefine mensaje rutas en función de enrutamiento de reglas toocontrol, donde el concentrador envía mensajes del dispositivo a la nube. Las reglas de enrutamiento no requieren toowrite cualquier código y pueden tener lugar de Hola de distribuidores de mensajes personalizados de posterior a la recopilación.

* **Supervisión de operaciones de conectividad del dispositivo**. Puede recibir registros de operación detallados sobre operaciones de administración de identidad de dispositivos y eventos de conectividad de dispositivos. Esta función de supervisión permite a los problemas de conectividad de IoT solución tooidentify, como los dispositivos que intente tooconnect con credenciales incorrectas, enviar mensajes con demasiada frecuencia o rechazar todos los mensajes en la nube al dispositivo.

* **Amplio conjunto de bibliotecas de dispositivos**. Los [SDK de dispositivo IoT de Azure][lnk-device-sdks] están disponibles y son compatibles con varios lenguajes y plataformas: C para muchas distribuciones de Linux, Windows y sistemas operativos en tiempo real. Los SDK de dispositivos IoT de Azure admiten lenguajes administrados como C#, Java y JavaScript.

* **Extensibilidad y protocolos de IoT**. Si la solución no utiliza las bibliotecas de dispositivo de hello, centro de IoT expone un protocolo público que permite a dispositivos toonatively uso hello MQTT v3.1.1, HTTP 1.1 o protocolos de AMQP 1.0. También puede extender toosupport centro de IoT para protocolos personalizados por:

  * Crear una puerta de enlace de campo con [Azure IoT borde] [ lnk-iot-edge] que convierte su tooone de protocolo personalizado de hello tres protocolos entienden por centro de IoT.
  * Hola personalizar [puerta de enlace de IoT de Azure protocolo][protocol-gateway], un componente de código abierto que se ejecuta en la nube de Hola.

* **Escala**. Centro de IoT de Azure escala toomillions de dispositivos conectados al mismo tiempo y millones de eventos por segundo.

## <a name="gateways"></a>Puertas de enlace

Una puerta de enlace en una solución de IoT es normalmente un [puerta de enlace de protocolo] [ lnk-iotedge] que se haya implementado en la nube de Hola o [puerta de enlace de campo] [ lnk-field-gateway] es decir implementado de forma local con los dispositivos. Una puerta de enlace de protocolo realiza la traducción de protocolos, por ejemplo MQTT tooAMQP. Una puerta de enlace de campo puede ejecutar análisis en el borde de hello, tomar decisiones de sujetos a limitación temporal tooreduce latencia, proporcionar servicios de administración de dispositivos, aplicar restricciones de privacidad y seguridad y realizará la traducción de protocolos. Ambos tipos de puerta de enlace actúan como intermediarios entre los dispositivos y el Centro de IoT.

Una puerta de enlace de campo es diferente de un dispositivo de enrutamiento de tráfico simple (como un firewall o un dispositivo de traducción de direcciones de red) porque normalmente desempeña un rol activo en la administración del acceso y del flujo de la información en su solución.

Una solución puede incluir tanto puertas de enlace de protocolo como de campo.

## <a name="how-does-iot-hub-work"></a>¿Cómo funciona el Centro de IoT?

Centro de IoT de Azure implementa hello [asistidas por el servicio de comunicación] [ lnk-service-assisted-pattern] back-end de las interacciones de patrón toomediate Hola entre los dispositivos y la solución. objetivo de Hola de comunicación asistidas por el servicio es tooestablish vías de comunicación de confianza bidireccional entre un sistema de control, como centro de IoT y dispositivos de propósito especial que se implementan en espacio físico no es de confianza. patrón de Hello establece Hola siguientes principios:

* La seguridad tiene prioridad sobre el resto de las funciones.

* Los dispositivos no aceptan información de redes no solicitadas. Un dispositivo establece todas las conexiones y las rutas en modo de solo salida. Para un dispositivo se tooreceive un comando de back-end de soluciones de hello, dispositivo Hola debe iniciarse con regularidad un toocheck de conexión para cualquier tooprocess de comandos pendientes.

* Solo deben conectarse dispositivos tooor establecer servicios toowell conocidos de las rutas que estén al mismo nivel, como centro de IoT.

* ruta de comunicación de Hello entre dispositivos y servicios o entre dispositivos y puerta de enlace se protege en la capa del protocolo de aplicación Hola.

* La autenticación y la autorización de nivel de sistema se basan en las identidades de cada dispositivo. Hacen los permisos y las credenciales de acceso revocables casi al instante.

* Se facilita la comunicación bidireccional para dispositivos que se conectan de forma esporádica due toopower o problemas de conectividad, se conservan los comandos y notificaciones de dispositivo hasta que un dispositivo conecta tooreceive ellos. Centro de IoT mantiene colas específico del dispositivo para los comandos de Hola que envía.

* Datos de carga de la aplicación está protegidos por separado para tránsito protegido a través del servicio determinado tooa de puertas de enlace.

Hello sector móvil usado por modelo de comunicación asistidas por el servicio de hello en servicios de notificación de inserción de gran escala tooimplement como [servicios de notificaciones de inserción de Windows][lnk-wns], [De mensajería de nube de Google][lnk-google-messaging], y [servicio de notificaciones de inserción de Apple][lnk-apple-push].

IoT Hub es compatible con la ruta de acceso de emparejamiento público de ExpressRoute.

## <a name="next-steps"></a>Pasos siguientes

vea toolearn cómo toosend mensajes desde un dispositivo y recibirlos desde el centro de IoT, así como cómo enruta el mensaje de tooconfigure, [enviar y recibir mensajes con el centro de IoT][lnk-send-messages].

toolearn cómo centro de IoT permite la administración de dispositivos basada en estándares tooremotely administrar, configurar y actualizar los dispositivos, consulte [información general de administración de dispositivos con el centro de IoT][lnk-device-management].

tooimplement las aplicaciones de cliente en una amplia variedad de plataformas de hardware de dispositivos y sistemas operativos, puede usar dispositivos de IoT de Azure de hello SDK. dispositivo de Hello SDK incluye bibliotecas que facilitan el envío telemetría tooan IoT hub y la recepción en la nube al dispositivo de mensajes. Cuando se utilizan dispositivos de hello SDK, puede elegir entre diversos toocommunicate de protocolos de red con el centro de IoT. toolearn más información, vea hello [obtener información acerca del dispositivo SDK][lnk-device-sdks].

tooget iniciado escribiendo código y ejecutar algunos ejemplos, vea hello [empezar a trabajar con el centro de IoT] [ lnk-get-started] tutorial.

[img-architecture]: media/iot-hub-what-is-iot-hub/hubarchitecture.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[protocol-gateway]: https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md
[lnk-service-assisted-pattern]: http://blogs.msdn.com/b/clemensv/archive/2014/02/10/service-assisted-communication-for-connected-devices.aspx "Comunicación asistida por servicios, publicación de blog de Clemens Vasters"
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-iotedge]: iot-hub-protocol-gateway.md
[lnk-field-gateway]: iot-hub-devguide-endpoints.md#field-gateways
[lnk-devguide-identityregistry]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-wns]: https://msdn.microsoft.com/library/windows/apps/mt187203.aspx
[lnk-google-messaging]: https://developers.google.com/cloud-messaging/
[lnk-apple-push]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-send-messages]: iot-hub-devguide-messaging.md
[lnk-device-management]: iot-hub-device-management-overview.md

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-security-ground-up]: iot-hub-security-ground-up.md
