---
title: aaaSecuring su Internet de las cosas de hello masa seguridad | Documentos de Microsoft
description: "Este artículo describen características de seguridad integradas de Hola de hello Microsoft Azure IoT Suite"
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 10252dfa-8313-4a97-9bd6-a3f1345dd3be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: a97e8cea753641e1e3c895f44e3fde1e5739d665
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-from-hello-ground-up"></a>Seguridad de Internet de las cosas de hello masa
Hola Internet de las cosas (IoT) representa un único seguridad, privacidad y cumplimiento desafíos toobusinesses en todo el mundo. A diferencia de la tecnología de intrusos tradicional donde estos problemas giran en torno a software y cómo se implementa, IoT está relacionado con lo que ocurre cuando los universos físico de Hola y Hola intrusos convergen. Proteger soluciones IoT requiere garantizar seguro de aprovisionamiento de dispositivos, una conexión segura entre estos dispositivos y la nube hello y la protección de proteger los datos en la nube de Hola durante el procesamiento y almacenamiento. Sin embargo, trabajar con esta funcionalidad tiene sus inconvenientes: la limitación de recursos de los dispositivos, la distribución geográfica de las implementaciones y la existencia de un gran número de dispositivos dentro de una solución.

Este artículo explora cómo Hola Microsoft Azure IoT Suite proporciona una solución de nube de Internet de las cosas segura y privada. Hello Azure IoT Suite proporciona una completa solución de-to-end, con la seguridad integrada en cada etapa de hello masa. En Microsoft, desarrollar software seguro forma parte de las prácticas de ingeniería de software de hello, cuya raíz comienza en nuestro décadas larga experiencia de desarrollo de software seguro. tooensure, ciclo de vida de desarrollo de seguridad (SDL) es la metodología de desarrollo fundamentales de hello, junto con un host de servicios de seguridad de nivel de infraestructura como hello unidad de crímenes digitales de Microsoft y la garantía de seguridad operativa (OSA) Microsoft Security Response Center y Microsoft Malware Protection Center. 

Hola únicos características de ofertas de conjunto de IoT de Azure, que hace el aprovisionamiento, conectarse a y almacenar datos de los dispositivos de IoT fáciles y transparentes y, sobre todo, seguro. En este artículo, examinaremos las características de seguridad de Azure IoT Suite hello e implementación estrategias tooensure seguridad, privacidad y cumplimiento desafíos se tratan. 

## <a name="introduction"></a>Introducción
Hola Internet de las cosas (IoT) es wave Hola de hello futura, las empresas inmediatas de la oferta y los costos de las oportunidades reales tooreduce, aumentar los ingresos y transformar su negocio. Muchas empresas, sin embargo, son toodeploy púbica IoT en sus organizaciones due tooconcerns sobre seguridad, privacidad y cumplimiento. Un punto principal de preocupación procede de unicidad de Hola de infraestructura de IoT hello, que combina intrusos hello y mundos físicos juntos, crear uno compuesto individuales riesgos inherentes en estos dos mundos. Seguridad de IoT pertenece integridad de hello tooensuring de código ejecutan en dispositivos, que proporciona autenticación de usuarios y dispositivos, definir la propiedad clara de dispositivos (así como los datos generados por los dispositivos) y que se va a toocyber resistente y ataques físicos. 

A continuación, no hay problema Hola de privacidad. Las empresas quieren transparencia en la recopilación de datos: qué se recopila y por qué, quién puede verlo, quién controla el acceso, etc. Por último, hay problemas de seguridad general de los equipos de hello junto con personas de hello operativo ellos y problemas de mantenimiento de los estándares del sector de cumplimiento de normas.

Dados Hola seguridad, privacidad, transparencia y problemas de cumplimiento, elegir el proveedor de soluciones de hello derecho IoT sigue siendo un desafío. Unir las piezas individuales de IoT software y servicios proporcionados por una variedad de proveedores presenta deficiencias en la seguridad, privacidad, transparencia y compatibilidad que puede ser toodetect de disco duro, sin olvidar corregir. elección de Hello de la derecha de hello IoT proveedor de software y el servicio se basa en encontrar los proveedores que tienen una amplia experiencia en la ejecución de servicios que abarcan verticales y regiones geográficas, pero también son tooscale capaz de una manera segura y transparente. Del mismo modo, es útil para saludo seleccionado proveedor toohave décadas de experiencia con el desarrollo de software seguro que se ejecuta en miles de millones de equipos en todo el mundo y ha panorama de amenazas de hello capacidad tooappreciate Hola que supone este nuevo mundo de hello Internet de Cosas.

## <a name="secure-infrastructure-from-hello-ground-up"></a>Infraestructura segura de hello masa
Hola [Microsoft Cloud](https://www.microsoft.com/enterprise/microsoftcloud/default.aspx#fbid=WzBsRQi6aGk) infraestructura admite los clientes de más de mil millones de 127 países. Dibujar en nuestra experiencia décadas larga compilar software de la empresa y algunas de Hola ejecutar servicios en línea más grandes en Hola a todos, proporcionamos niveles más altos de mejorar la seguridad, privacidad, cumplimiento y amenaza prácticas recomendadas de mitigación que podría la mayoría de los clientes lograr por sí solas.

Nuestro [del ciclo de vida de desarrollo de seguridad (SDL)](https://www.microsoft.com/sdl/) proporciona un proceso de desarrollo obligatoria de toda la empresa con requisitos de seguridad en el ciclo de vida de hello todo el software. toohelp asegurarse de que las actividades operativas seguir Hola mismo nivel de prácticas de seguridad, usamos directrices de seguridad rigurosa dispuestas en el proceso de garantía de seguridad operativa (OSA). Trabajamos también con las firmas de auditoría de terceros para la comprobación en curso que cumplimos nuestras obligaciones de cumplimiento de normas y participar en los esfuerzos de seguridad amplia a través de la creación de hello de centros de excelencia, incluidos Hola unidad de crímenes digitales de Microsoft, Microsoft Security Centro de respuestas y Microsoft Malware Protection Center.

## <a name="microsoft-azure---secure-iot-infrastructure-for-your-business"></a>Microsoft Azure: infraestructura de IoT segura para su negocio
Microsoft Azure ofrece una solución completa en la nube, que combina una colección creciente de servicios en la nube integrado: análisis, aprendizaje automático, almacenamiento, seguridad, red y web, con una protección de toohello de compromiso líderes en la industria y la privacidad de los datos. Nuestro [suponga infracción](https://azure.microsoft.com/blog/red-teaming-using-cutting-edge-threat-simulation-to-harden-the-microsoft-enterprise-cloud/) estrategia utiliza un dedicado "rojo equipo" de expertos de seguridad de software que simular ataques, pruebas de capacidad de Hola de Azure toodetect, protección contra amenazas y recuperarse de infracciones. Nuestro [respuesta a incidentes global](https://www.microsoft.com/TrustCenter/Security/DesignOpSecurity) resuelve de equipo de hello reloj efectos de hello toomitigate de ataques y actividades malintencionadas. equipo de Hello sigue los procedimientos ya establecidos para la administración de incidentes, la comunicación y la recuperación y utiliza las interfaces reconocibles y predecibles con socios internos y externos.

Nuestros sistemas proporcionan continua detección y prevención de intrusiones, prevención de ataques de servicio, pruebas de penetración periódicas y herramientas forenses que ayudan a identificar y reducir las amenazas. [La autenticación multifactor](../multi-factor-authentication/multi-factor-authentication.md) proporciona un nivel adicional de seguridad para los usuarios finales tooaccess Hola red. Y para la aplicación hello y proveedor de host de hello, ofrecemos el control de acceso, supervisión, antimalware, examen de las vulnerabilidades, revisiones y administración de configuración.

Hola Microsoft Azure IoT Suite aprovecha las ventajas de seguridad de Hola y privacidad integran Hola plataforma Windows Azure junto con los procesos SDL y OSA para desarrollo seguro y el funcionamiento de todo el software de Microsoft. Estos procedimientos proporcionan protección de la infraestructura, protección de red y seguridad de toohello fundamentales de características de administración de identidades y de cualquier solución. 

Hola [centro de IoT de Azure](../iot-hub/iot-hub-what-is-iot-hub.md) en hello [Suite IoT](iot-suite-what-is-azure-iot.md) ofrece un servicio completamente administrado que permite la comunicación bidireccional confiable y segura entre los dispositivos de IoT y servicios de Azure como [Aprendizaje automático de azure](../machine-learning/machine-learning-what-is-machine-learning.md) y [análisis de transmisiones de Azure](../stream-analytics/stream-analytics-introduction.md) mediante el uso de credenciales de seguridad por dispositivo y control de acceso.

toobest comunicarse características de seguridad y privacidad integradas en hello Suite de IoT de Azure, nos hemos desglosado suite hello en tres áreas de seguridad principal Hola. 

![Conjunto de aplicaciones de IoT de Azure](media/securing-iot-ground-up/securing-iot-ground-up-fig3.png)

### <a name="secure-device-provisioning-and-authentication"></a>Seguridad en el aprovisionamiento y la autenticación de dispositivos
Hello Azure IoT Suite protege dispositivos mientras están en el campo de hello proporcionando una clave de identidad única para cada dispositivo, que puede utilizar Hola IoT infraestructura toocommunicate con dispositivos de Hola de mientras está en funcionamiento. proceso de Hello es rápido y fácil tooset seguridad. Hola clave generada con una base de Hola de formularios de dispositivo seleccionados por el usuario Id. de un token que se utiliza en todas las comunicaciones entre el dispositivo de Hola y Hola centro de IoT de Azure.

Los identificadores de dispositivo se puede asociar a un dispositivo durante la fabricación (es decir, se vacían en un módulo de confianza de hardware) o pueden usar una identidad fija existente como proxy (por ejemplo, los números de serie de CPU). Puesto que no es sencillo cambiar esta información de identificación en el dispositivo de hello, es importante toointroduce identificadores de dispositivo lógico en caso de cambios de hardware de dispositivo subyacente Hola pero sigue siendo de dispositivo lógico de Hola Hola igual. En algunos casos, puede ocurrir asociación Hola de una identidad de dispositivo en tiempo de implementación de dispositivo (es decir, un ingeniero de campo autenticado físicamente configura un nuevo dispositivo al comunicarse con el back-end de hello solución). Hola [del registro de la identidad de centro de IoT de Azure](../iot-hub/iot-hub-devguide.md) ofrece un almacenamiento seguro de identidades de dispositivos y las claves de seguridad para una solución. Pueden agregarse individuales o grupos de identidades de dispositivos tooan Permitir lista o una lista de bloqueo, lo que permite un control completo sobre el acceso a los dispositivos.

Directivas de control de acceso de Azure centro de IoT en nube Hola habilitan la activación y desactivación de cualquier identidad del dispositivo, proporciona una manera toodisassociate un dispositivo de una implementación de IoT cuando sea necesario. Esta asociación y desasociación de dispositivos se basa en la identidad de cada dispositivo.

Características de seguridad de dispositivo adicionales Hola siguientes:

* Los dispositivos no aceptan conexiones de red no solicitadas. Establecen todas las conexiones y rutas solo en modo saliente. Para un dispositivo se tooreceive un comando de back-end de hello, dispositivo Hola debe iniciar una toocheck de conexión para cualquier tooprocess de comandos pendientes. Una vez establecida una conexión entre el dispositivo de Hola y centro de IoT la forma segura, mensajería de nube toohello dispositivo de Hola y toohello de dispositivo en la nube puede enviarse forma transparente.  
* Dispositivos solo conectan tooor establecer las rutas conocidas de toowell servicios con el que estén al mismo nivel, como un centro de IoT de Azure.
* En la autenticación y la autorización de nivel de sistema se emplean las identidades de cada dispositivo, lo que hace que las credenciales y los permisos de acceso se puedan revocar casi de manera instantánea.

### <a name="secure-connectivity"></a>Conectividad segura
La durabilidad de la mensajería es una característica importante de cualquier solución IoT. Hello necesita especificar toodurably entregar comandos y recibir datos de dispositivos está subrayado por hecho de Hola que IoT dispositivos se conectan a través Internet hello, u otras redes similar que pueden ser poco confiables. Centro de IoT de Azure ofrece la durabilidad de mensajería entre la nube y los dispositivos a través de un sistema de confirmaciones en respuesta toomessages. Durabilidad adicional para la mensajería se logra mediante mensajes del almacenamiento en caché de hello centro de IoT para los días de tooseven de telemetría y dos días para los comandos.

Eficacia es importante tooensure conservación de recursos y las operaciones en un entorno con recursos limitados. HTTPS (HTTP seguro), versión segura de hello estándar del sector del protocolo http populares de hello, es compatible con el centro de IoT de Azure, lo que permite una comunicación eficaz. Advanced Message Queuing Protocol (AMQP) y Message Queuing Telemetry Transport (MQTT), admitidos en el Centro de IoT de Azure, están diseñados no solo para la eficacia en términos del uso de recursos, sino también para la entrega confiable de mensajes. 

Escalabilidad requiere hello toosecurely de capacidad para interactuar con una amplia gama de dispositivos. Centro de IoT de Azure permite la conexión segura tooboth los dispositivos habilitados para IP y no IP habilitado. Dispositivos habilitados para IP son toodirectly capaz de conectarse y comunicarse con el centro de IoT de Hola a través de una conexión segura. Los dispositivos no habilitados para IP están limitados por los recursos y solo se conectan mediante protocolos de comunicación de corta distancia, como Zwave, ZigBee y Bluetooth. Una puerta de enlace de campo es tooaggregate utilizado en estos dispositivos y realiza el protocolo traducción tooenable bidireccional una comunicación segura con la nube de Hola.

Características de seguridad de conexión adicionales Hola siguientes:

* Hello ruta de comunicación entre los dispositivos y centro de IoT de Azure, o entre las puertas de enlace y centro de IoT de Azure, se protege utilizando seguridad estándar del sector de capa de transporte (TLS) con el centro de IoT de Azure autentica utilizando el protocolo X.509.
* En dispositivos de tooprotect de orden de las conexiones entrantes no solicitadas, centro de IoT de Azure no se abre cualquier dispositivo de toohello de conexión. dispositivo de Hello inicia todas las conexiones. 
* Centro de IoT de Azure forma duradera almacena los mensajes para los dispositivos y espera Hola dispositivo tooconnect. Estos comandos se almacenan durante dos días, habilitar los dispositivos que se conectan de forma esporádica, debido a problemas de conectividad o toopower, tooreceive estos comandos. El Centro de IoT de Azure mantiene una cola por dispositivo para cada dispositivo.

### <a name="secure-processing-and-storage-in-hello-cloud"></a>El procesamiento seguro y el almacenamiento en nube de Hola
De datos de tooprocessing de comunicaciones cifradas en la nube de hello, hello Azure IoT Suite le ayuda a proteger los datos. Proporciona flexibilidad tooimplement más sistemas de cifrado y administración de claves de seguridad. Con Azure Active Directory (AAD) para la autorización y autenticación de usuario, conjunto de IoT de Azure puede proporcionar un modelo de autorización basada en directivas para los datos en la nube de hello, habilitar la administración de facilitar el acceso que se pueden auditar y revisar. Este modelo también permite casi instantánea revocación de acceso toodata en la nube de Hola y de los dispositivos conectados toohello Suite de IoT de Azure.

Una vez que los datos están en la nube de hello, puede procesar y almacenado en cualquier flujo de trabajo definido por el usuario. Parte de tooeach de acceso de datos de Hola se controla con Azure Active Directory, dependiendo de servicio de almacenamiento de hello utilizado.

Todas las claves Hola IoT infraestructura utilizadas se almacenan en la nube de hello en un almacenamiento seguro, con hello tooroll de capacidad sobre en caso de que las claves necesitan toobe vuelven a aprovisionar. Datos pueden almacenarse en [base de datos de Azure Cosmos](../documentdb/documentdb-introduction.md) o en [bases de datos SQL](../sql-database/sql-database-faq.md), habilitar la definición de nivel de Hola de seguridad deseado. Además, Azure proporciona una manera toomonitor y auditar todos los acceso tooyour datos tooalert de intrusión o acceso no autorizado.

## <a name="conclusion"></a>Conclusión
Hello Internet de las cosas se inicia con tus cosas: Hola, lo que importa toobusinesses mayoría. IoT puede entregar increíbles business tooa de valor se reducen los costos, aumentar los ingresos y transformación empresarial. Éxito de esta transformación depende en gran medida elegir Hola derecho IoT software y proveedor de servicios. Eso significa encontrar un proveedor que no solo comprenda las necesidades y los requisitos de la empresa para hacer posible esta transformación, sino que también proporcione servicios y software en los que la seguridad, la privacidad, la transparencia y el cumplimiento integrados sean las consideraciones de diseño principales. Microsoft tiene una amplia experiencia con el desarrollo e implementación de software seguro y los servicios y continúa toobe líder en esta nueva era de Internet de las cosas. 

Hola Microsoft Azure IoT Suite se basa en las medidas de seguridad de forma predeterminada, habilitar la supervisión de seguros de las eficiencias tooimprove de activos, impulsar la innovación de tooenable de rendimiento operativa y emplean avanzado análisis de datos tootransform empresas. Con su enfoque por capas para patrones de diseño, seguridad y varias características de seguridad, conjunto de IoT de Azure le ayuda a implementar una infraestructura que puede ser de confianza tootransform las empresas. 

## <a name="additional-information"></a>Información adicional
Cada solución preconfigurada de conjunto de IoT de Azure crea instancias de servicios de Azure, como siguiente hello:

* [**Centro de IoT de Azure**](https://azure.microsoft.com/services/iot-hub/): la puerta de enlace que se conecta en la nube Hola demasiado "acciones". Puede escalar toomillions de conexiones por concentrador y proceso de grandes volúmenes de datos con compatibilidad con la autenticación por dispositivo ayudarle a proteger la solución.
* [**Base de datos de Azure Cosmos**](https://azure.microsoft.com/services/documentdb/): un servicio de base de datos escalable e indexan completamente para datos semiestructurados que administra los metadatos para los dispositivos de hello aprovisionar, como atributos, configuración y propiedades de seguridad. Cosmos DB ofrece procesamiento de alto rendimiento, indexación de datos independiente del esquema y una completa interfaz de consultas SQL.
* [**Análisis de transmisiones de Azure**](https://azure.microsoft.com/services/stream-analytics/): transmisiones en tiempo real de procesamiento en la nube de Hola que permite toorapidly desarrollar e implementar una visión análisis de bajo costo solución toouncover en tiempo real de dispositivos, sensores, la infraestructura de y aplicaciones. datos de Hola desde este servicio completamente administrado pueden reducir el volumen de tooany bien con un alto rendimiento, baja latencia y la resistencia.
* [**Servicios de aplicaciones de Azure**](https://azure.microsoft.com/services/app-service/): un sitio web eficaz toobuild plataforma de nube y aplicaciones móviles que se conectan en cualquier lugar; toodata en la nube de Hola o de forma local. Cree atractivas aplicaciones móviles para iOS, Android y Windows. Integrar con el Software como servicio (SaaS) y enterprise las aplicaciones con toodozens cuadro conectividad de servicios en la nube y aplicaciones empresariales. El código en su lenguaje preferido y el IDE:. NET, Node.js, PHP, Python o Java: toobuild las aplicaciones web y las API más rápido que nunca.
* [**Lógica de aplicaciones**](https://azure.microsoft.com/services/app-service/logic/): característica de Logic Apps Hola de servicio de aplicaciones de Azure le ayuda a integrar sus sistemas de línea de negocio existentes de IoT solución tooyour y automatizar los procesos de flujo de trabajo. Lógica de aplicaciones permite que los flujos de trabajo a los desarrolladores toodesign que comienzan con un desencadenador y, a continuación, ejecutan una serie de pasos, reglas y acciones que usan toointegrate conectores eficaces con los procesos empresariales. Lógica de aplicaciones ofrece gran ecosistema de tooa de conectividad de cuadro de SaaS, basada en la nube y aplicaciones locales.
* [**Almacenamiento de blobs de Azure**](https://azure.microsoft.com/services/storage/): almacenamiento en nube rentable, confiable para los datos de Hola que los dispositivos envían toohello en la nube.

## <a name="next-steps"></a>Pasos siguientes
toolearn más acerca de cómo proteger la solución de IoT, vea:

* [Procedimientos recomendados para la seguridad de IoT][lnk-security-best-practices]
* [Arquitectura de seguridad de IoT][lnk-security-architecture]
* [Protección de su implementación de IoT][lnk-security-deployment]

[lnk-security-best-practices]: iot-security-best-practices.md
[lnk-security-architecture]: iot-security-architecture.md
[lnk-security-deployment]: iot-suite-security-deployment.md

También puede explorar algunas de hello otras características y capacidades de hello IoT preconfigurado soluciones:

* [Información general de la solución preconfigurada de mantenimiento predictivo][lnk-predictive-overview]
* [Preguntas más frecuentes sobre el Conjunto de aplicaciones de IoT][lnk-faq]

Puede leer acerca de la seguridad del centro de IoT [tooIoT de acceso de Control concentrador] [ lnk-devguide-security] Hola Guía del desarrollador de centro de IoT.

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md
