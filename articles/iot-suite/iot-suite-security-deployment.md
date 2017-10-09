---
title: "aaaSecure la implementación de Internet de las cosas | Documentos de Microsoft"
description: "Este artículo detalles de cómo toosecure la implementación de IoT"
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 95c23341-16b0-4954-b3f2-d2e82ab7b367
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: befba8f2009279c2217dcd3496d529139134ec01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-iot-deployment"></a>Proteger su implementación de IoT
Este artículo ofrece Hola siguiente nivel de detalle para proteger la infraestructura de hello basado en Azure IoT Internet de las cosas (IoT). Incluye vínculos a los detalles de nivel de tooimplementation para configurar e implementar cada componente. También se proporcionan comparaciones y opciones entre diversos métodos que compiten entre sí.

Protección de la implementación de Azure IoT Hola puede dividirse en hello siguientes tres áreas de seguridad:

* **Seguridad de los dispositivos**: protección de dispositivos de IoT de hello mientras se implementa en hello comodín.
* **Seguridad de conexión**: asegurarse de todos los datos transmitidos entre dispositivos de IoT de Hola y centro de IoT es confidencial y prueba de manipulaciones.
* **Seguridad en la nube**: proporcionando un medio toosecure datos mientras se mueve a través de y se almacena en la nube de Hola.

![Tres áreas de seguridad][img-overview]

## <a name="secure-device-provisioning-and-authentication"></a>Seguridad en el aprovisionamiento y la autenticación de dispositivos
Hello Azure IoT Suite protege los dispositivos de IoT por hello siguiendo dos métodos:

* Al proporcionar una clave de identidad única (tokens de seguridad) para cada dispositivo, lo que puede usarse en hello dispositivo toocommunicate con hello centro de IoT.
* Mediante el uso de un dispositivo [certificado X.509] [ lnk-x509] y la clave privada como una toohello de dispositivo de medios tooauthenticate Hola centro de IoT. Este método de autenticación garantiza que Hola clave privada en el dispositivo de Hola se desconoce fuera de dispositivo de Hola en cualquier momento, proporcionar un mayor nivel de seguridad.

método de token de seguridad de Hello proporciona autenticación para las llamadas realizadas por hello dispositivo tooIoT concentrador mediante la asociación de llamada de hello tooeach clave simétrica. Autenticación basada en X.509 permite la autenticación de un dispositivo de IoT en nivel físico de hello como parte del establecimiento de la conexión TLS Hola. método basado en tokens de seguridad de Hola se puede utilizar sin autenticación de X.509 Hola que es un patrón de menos seguro. Hello elegir entre métodos de hello dos es principalmente dictado por Hola de forma segura la autenticación de dispositivo debe toobe y la disponibilidad de almacenamiento seguro en el dispositivo de Hola (toostore Hola clave privada segura).

## <a name="iot-hub-security-tokens"></a>Tokens de seguridad del Centro de IoT
Centro de IoT usa seguridad tokens tooauthenticate dispositivos y servicios tooavoid envío de claves de red de Hola. Además, los tokens de seguridad están limitados en cuanto al ámbito y el período de validez. Los SDK de IoT de Azure generan automáticamente tokens sin necesidad de ninguna configuración especial. Sin embargo, algunos escenarios, requieren Hola usuario toogenerate y utilizar directamente los tokens de seguridad. Puede tratarse uso directo de Hola de superficies de hello MQTT, AMQP o HTTP o implementación de hello del modelo de servicio de token de Hola.

Obtener más detalles sobre la estructura de Hola de token de seguridad de Hola y su uso pueden encontrarse en hello siguientes artículos:

* [Estructura del token de seguridad][lnk-security-tokens]
* [Uso de tokens de SAS como dispositivo][lnk-sas-tokens]

Cada centro de IoT tiene un [del registro de identidad] [ lnk-identity-registry] que puede ser toocreate usado por dispositivo recursos en el servicio de hello, por ejemplo, una cola que contiene mensajes de nube al dispositivo en curso y tooallow acceso toohello puntos de conexión de dispositivo. Hola del registro de identidad de centro de IoT proporciona un almacenamiento seguro de identidades de dispositivos y las claves de seguridad para una solución. Pueden agregarse individuales o grupos de identidades de dispositivos tooan Permitir lista o una lista de bloqueo, lo que permite un control completo sobre el acceso a los dispositivos. Hello artículos siguientes proporcionan más detalles en la estructura de Hola de registro de la identidad de Hola y operaciones admitidas.

[IoT Hub admite protocolos como MQTT, AMQP y HTTP][lnk-protocols]. Cada uno de estos protocolos utilizan tokens de seguridad de hello IoT dispositivo tooIoT concentrador de forma diferente:

* AMQP: Seguridad de sin formato y basada en AMQP notificaciones SASL ({policyName}@sas.root. {} iothubName} en caso de hello de tokens de nivel del centro de IoT; {deviceId} en el caso de tokens centrada en el dispositivo).
* MQTT: Conectar utiliza paquetes {deviceId} como Hola {ClientId}, {IoThubhostname} / {deviceId} en hello **nombre de usuario** campo y una SAS de token en hello **contraseña** campo.
* HTTP: Símbolo (token) válido es en el encabezado de solicitud de autorización de Hola.

Registro de la identidad de centro de IoT puede credenciales de seguridad de tooconfigure usado por el dispositivo y el control de acceso. Sin embargo, si una solución de IoT ya realizó una inversión importante en un [Registro de identidad del dispositivo o un esquema de autenticación personalizados][lnk-custom-auth], se puede integrar en una infraestructura existente con IoT Hub mediante la creación de un servicio de token.

### <a name="x509-certificate-based-device-authentication"></a>Autenticación de dispositivos basada en certificados X.509
Hola de uso de un [basado en dispositivos certificado X.509] [ lnk-protocols] y su par de claves pública y privada asociado permite autenticación adicional en el nivel físico Hola. clave privada de Hola se almacena de forma segura en el dispositivo de hello y no es reconocible fuera Hola dispositivo. certificado X.509 de Hello contiene información acerca del dispositivo de hello, como Id. de dispositivo y otros detalles de la organización. Una firma de certificado de Hola se genera mediante la clave privada de Hola.

Flujo de aprovisionamiento de dispositivos de alto nivel:

* Asociar un identificador tooa dispositivo físico: identidad del dispositivo o dispositivos de toohello asociados de certificado X.509 durante dispositivos de fabricación o puesta en servicio.
* Crear una entrada de identidad correspondiente en el centro de IoT: identidad del dispositivo y la información de dispositivo asociado en hello del registro de identidad de centro de IoT.
* Almacenar la huella digital del certificado X.509 de forma segura en el Registro de identidad de IoT Hub.

### <a name="root-certificate-on-device"></a>Certificado raíz en el dispositivo
Al establecer una conexión segura de TLS con el centro de IoT, dispositivos de IoT Hola autentica utilizando un certificado raíz que forma parte del SDK de dispositivos de Hola de centro de IoT. Para SDK de cliente de hello C certificado Hola se encuentra en la carpeta de Hola "\\c\\certificados" bajo raíz de hello del repositorio de Hola. A pesar de que estos certificados raíz son de larga duración, puede caducar o revocarse. Si no hay ninguna manera de actualizar certificado de hello en dispositivo hello, hello dispositivo no podrá conectarse toosubsequently toohello centro de IoT (o cualquier otro servicio de nube). Tener un certificado de raíz de medios tooupdate Hola una vez implementado dispositivos de IoT Hola mitigará eficazmente este riesgo.

## <a name="securing-hello-connection"></a>Proteger conexión Hola
Conexión a Internet entre dispositivos de IoT de Hola y centro de IoT se protege utilizando Hola estándar de seguridad de capa de transporte (TLS). IoT de Azure admite [TLS 1.2][lnk-tls12], TLS 1.1 y TLS 1.0, en este orden. La compatibilidad con TLS 1.0 solo se proporciona para permitir versiones anteriores. Se recomienda toouse TLS 1.2, puesto que ofrece Hola seguridad mayoría.

Conjunto de IoT de Azure admite Hola siguiendo conjuntos de cifrado, en este orden.

| Conjunto de cifrado | Length |
| --- | --- |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384 (0xc028) ECDH secp384r1 (eq. RSA de 7680 bits) FS |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0xc027) ECDH secp256r1 (eq. RSA de 3072 bits) FS |128 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA (0xc014) ECDH secp384r1 (eq. RSA de 7680 bits) FS |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA (0xc013) ECDH secp256r1 (eq. RSA de 3072 bits) FS |128 |
| TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0x9d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256 (0x9c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA256 (0x3d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0x3c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA (0x35) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA (0x2f) |128 |
| TLS\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA (0xa) |112 |

## <a name="securing-hello-cloud"></a>Protección de nube de Hola
Azure IoT Hub permite la definición de [directivas de control de acceso][lnk-protocols] para cada clave de seguridad. Usa Hola siguiendo el conjunto de permisos toogrant acceso tooeach de extremos del centro de IoT. Permisos limitan Hola acceso tooan que centro de IoT basado en la funcionalidad.

* **RegistryRead**. Registro de identidad de toohello de concede acceso de lectura. Para más información, consulte [Registro de identidad][lnk-identity-registry].
* **RegistryReadWrite**. Concede acceso de lectura y escritura toohello del registro de identidad. Para más información, consulte [Registro de identidad][lnk-identity-registry].
* **ServiceConnect**. Concede acceso toocloud orientada a servicios comunicación y supervisión de los puntos de conexión. Por ejemplo, concede permiso tooback-end en la nube servicios tooreceive dispositivo a la nube mensajes, enviar mensajes de la nube al dispositivo y Hola recuperar correspondientes confirmaciones de entrega.
* **DeviceConnect**. Concede acceso a extremos de acceso toodevice. Por ejemplo, se concede permiso mensajes del dispositivo a la nube de toosend y recibir mensajes en la nube al dispositivo. Este permiso lo usan los dispositivos.

Hay dos tooobtain formas **DeviceConnect** permisos con el centro de IoT con [tokens de seguridad][lnk-sas-tokens]: con una clave de identidad de dispositivo o una clave de acceso compartido. Además, es importante toonote toda la funcionalidad accesible desde dispositivos expuesto por diseño en los puntos de conexión con el prefijo `/devices/{deviceId}`.

[Componentes del servicio solo pueden generar tokens de seguridad] [ lnk-service-tokens] usar compartidos conceder los permisos adecuados de hello las directivas de acceso.

Centro de IoT de Azure y otros servicios que pueden formar parte de la solución de Hola que admita la administración de usuarios con hello Azure Active Directory.

Los datos consumidos por Azure IoT Hub se pueden usar en una gran variedad de servicios, como Azure Stream Analytics, Azure Blob Storage, etc. Estos servicios permiten el acceso de administración. Lea más sobre estos servicios y las opciones disponibles a continuación:

* [Base de datos de Azure Cosmos][lnk-docdb]: un servicio de base de datos escalable e indexan completamente para datos semiestructurados que administra los metadatos para los dispositivos de hello aprovisionar, como atributos, configuración y propiedades de seguridad. Cosmos DB ofrece procesamiento de alto rendimiento, indexación de datos independiente del esquema y una completa interfaz de consultas SQL.
* [Análisis de transmisiones de Azure][lnk-asa]: transmisiones en tiempo real de procesamiento en la nube de Hola que permite toorapidly desarrollar e implementar una visión análisis de bajo costo solución toouncover en tiempo real de los dispositivos, sensores, infraestructura y aplicaciones. datos de Hola desde este servicio completamente administrado pueden reducir el volumen de tooany bien con un alto rendimiento, baja latencia y la resistencia.
* [Servicios de aplicaciones de Azure][lnk-appservices]: un sitio web eficaz toobuild plataforma de nube y aplicaciones móviles que se conectan en cualquier lugar; toodata en la nube de Hola o de forma local. Cree atractivas aplicaciones móviles para iOS, Android y Windows. Integrar con el Software como servicio (SaaS) y enterprise las aplicaciones con toodozens cuadro conectividad de servicios en la nube y aplicaciones empresariales. El código en su lenguaje favorito y IDE toobuild (. NET, Node.js, PHP, Python o Java) las aplicaciones web y las API más rápidas que nunca.
* [Lógica de aplicaciones][lnk-logicapps]: característica de Logic Apps Hola de servicio de aplicaciones de Azure le ayuda a integrar sus sistemas de línea de negocio existentes de IoT solución tooyour y automatizar los procesos de flujo de trabajo. Lógica de aplicaciones permite que los flujos de trabajo a los desarrolladores toodesign que comienzan con un desencadenador y, a continuación, ejecutan una serie de pasos, reglas y acciones que usan toointegrate conectores eficaces con los procesos empresariales. Lógica de aplicaciones ofrece gran ecosistema de tooa de conectividad de cuadro de SaaS, basada en la nube y aplicaciones locales.
* [Almacenamiento de blobs de Azure][lnk-blob]: almacenamiento en nube rentable, confiable para los datos de Hola que los dispositivos envían toohello en la nube.

## <a name="conclusion"></a>Conclusión
En este artículo se proporciona información general sobre los detalles de los niveles de implementación para diseñar e implementar una infraestructura de IoT mediante IoT de Azure. Configurar cada toobe componente segura es clave para la protección de Hola toda la infraestructura de IoT. Opciones de diseño de Hello disponibles en IoT de Azure proporcionan un cierto nivel de flexibilidad y elección; Sin embargo, cada opción podría tener implicaciones de seguridad. Se recomienda valorar cada una de estas opciones mediante una evaluación de riesgo y costo.

## <a name="see-also"></a>Otras referencias
También puede explorar algunas de hello otras características y capacidades de hello IoT preconfigurado soluciones:

* [Información general de la solución preconfigurada de mantenimiento predictivo][lnk-predictive-overview]
* [Preguntas más frecuentes sobre el Conjunto de aplicaciones de IoT][lnk-faq]

Puede leer acerca de la seguridad del centro de IoT [tooIoT de acceso de Control concentrador] [ lnk-devguide-security] Hola Guía del desarrollador de centro de IoT.


[img-overview]: media/iot-suite-security-deployment/overview.png

[lnk-security-tokens]: ../iot-hub/iot-hub-devguide-security.md#security-token-structure
[lnk-sas-tokens]: ../iot-hub/iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-protocols]: ../iot-hub/iot-hub-devguide-security.md
[lnk-custom-auth]: ../iot-hub/iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: http://www.itu.int/rec/T-REC-X.509-201210-I/en
[lnk-tls12]: https://tools.ietf.org/html/rfc5246
[lnk-service-tokens]: ../iot-hub/iot-hub-devguide-security.md#use-security-tokens-from-service-components
[lnk-docdb]: https://azure.microsoft.com/services/documentdb/
[lnk-asa]: https://azure.microsoft.com/services/stream-analytics/
[lnk-appservices]: https://azure.microsoft.com/services/app-service/
[lnk-logicapps]: https://azure.microsoft.com/services/app-service/logic/
[lnk-blob]: https://azure.microsoft.com/services/storage/

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md
