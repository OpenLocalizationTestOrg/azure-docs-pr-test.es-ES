
# <a name="azure-and-internet-of-things"></a>Azure y el Internet de las cosas

Bienvenido tooMicrosoft Azure y Hola Internet de las cosas (IoT). Este artículo presenta una arquitectura de solución de IoT que describe las características comunes de Hola de una solución de IoT que podría implementar con los servicios de Azure. Soluciones de IoT requieren seguros, la comunicación bidireccional entre los dispositivos, posiblemente numeración de hello millones y un back-end de soluciones. Por ejemplo, un back-end de soluciones puede usar análisis predictivo, automatizada toouncover visión de la secuencia de eventos de dispositivo a la nube.

Azure IoT Hub es un componente fundamental cuando se implementa esta arquitectura de solución de IoT mediante servicios de Azure. El Conjunto de aplicaciones de IoT proporciona implementaciones completas y de un extremo a otro de esta arquitectura para escenarios de IoT específicos. Por ejemplo:

* Hola *supervisión remota* solución le permite toomonitor Hola estado de dispositivos como máquinas expendedoras.
* Hola *mantenimiento predictivo* solución le ayuda a las necesidades de mantenimiento de tooanticipate de dispositivos como bombas en estaciones de bombeo remotas y el tiempo de inactividad no programado de tooavoid.
* Hola *generador conectado* solución le ayuda a tooconnect y supervise sus dispositivos industriales.

## <a name="iot-solution-architecture"></a>Arquitectura de solución IoT

Hola siguiente diagrama muestra una arquitectura típica de solución de IoT. diagrama de Hello no incluye los nombres de Hola de los servicios de Azure específicos, pero describe Hola elementos clave en una arquitectura de solución de IoT genérica. En esta arquitectura, dispositivos de IoT recopilan los datos que envía tooa puerta de enlace de nube. puerta de enlace de nube de Hello hace Hola datos disponibles para el procesamiento por otros servicios back-end desde donde los datos se entregan las aplicaciones de línea de negocio de tooother o toohuman operadores a través de un panel u otro dispositivo de presentación.

![Arquitectura de solución IoT][img-solution-architecture]

> [!NOTE]
> Para obtener una explicación más detallada de la arquitectura de IoT, vea hello [arquitectura de referencia de Microsoft Azure IoT][lnk-refarch].

### <a name="device-connectivity"></a>Conectividad de dispositivos

En esta arquitectura de solución de IoT, dispositivos envían telemetría, como las lecturas de sensor desde una estación de bombeo, punto de conexión de tooa en la nube para el almacenamiento y procesamiento. En un escenario de un mantenimiento predictivo, back-end de soluciones de hello podría utilizar una secuencia de Hola de sensor datos toodetermine cuando una bomba específica requiere mantenimiento. Dispositivos también pueden recibir y responder mensajes toocloud al dispositivo mediante la lectura de mensajes desde un punto de conexión en la nube. Por ejemplo, hello mantenimiento predictivo solución del escenario Hola back-end puede enviar mensajes tooother bombas en hello bombeando toobegin estación reenrutamiento flujos justo antes del vencimiento mantenimiento toostart. Este procedimiento se Asegúrese de que el ingeniero de mantenimiento de hello podría empezar a trabajar en cuanto se llega.

Uno de los desafíos más grandes de Hola para proyectos de IoT es cómo tooreliably y conectarse de forma segura los dispositivos toohello solución back-end. Dispositivos de IoT tienen diferentes características como tooother comparados clientes como exploradores y aplicaciones móviles. Dispositivos IoT:

* A menudo son sistemas insertados sin operador humano.
* Se pueden implementar en ubicaciones remotas, donde el acceso físico resulta costoso.
* Solo puede ser accesible a través de hello solución back-end. No hay ningún otro toointeract manera con el dispositivo de Hola.
* Es posible que tengan limitaciones de recursos de procesamiento y alimentación.
* Es posible que tengan conectividad de red intermitente, lenta o costosa.
* Puede necesitar toouse protocolos de aplicación propios, personalizados o específicos del sector.
* Pueden crearse mediante un amplio conjunto de plataformas populares de hardware y software.

Además toohello requisitos anteriores, cualquier solución de IoT debe también ofrecen escalabilidad, seguridad y confiabilidad. Hola conjunto resultante de los requisitos de conectividad es difícil y tardar mucho tiempo tooimplement mediante tecnologías tradicionales como contenedores de web y agentes de mensajería. Hello y centro de IoT de Azure SDK de dispositivos de IoT de Azure que sea más fáciles soluciones tooimplement que cumplen estos requisitos.

Un dispositivo puede comunicarse directamente con un punto de conexión de puerta de enlace de nube, o si el dispositivo de hello no puede usar cualquiera de los protocolos de comunicaciones de Hola que Hola admite la puerta de enlace en la nube, puede conectarse a través de una puerta de enlace intermedia. Por ejemplo, hello [puerta de enlace de IoT de Azure protocolo] [ lnk-protocol-gateway] puede realizar la traducción de protocolos si los dispositivos no pueden usar cualquiera de los protocolos de Hola que admite el centro de IoT.

### <a name="data-processing-and-analytics"></a>Procesamiento de datos y análisis

En la nube de hello, un IoT solución back-end es donde se produce la mayor parte del procesamiento de datos de hello, como el filtrado y agregación de telemetría y enrutamiento tooother servicios. Hola IoT back-end de soluciones:

* Recibe la telemetría a escala de los dispositivos y determina cómo tooprocess y almacenar esos datos. 
* Puede permiten toosend comandos desde dispositivo toospecific de hello en la nube.
* Proporciona capacidades de registro de dispositivo que le permiten tooprovision dispositivos y los dispositivos que se permiten tooconnect tooyour infraestructura de toocontrol.
* Permite tootrack Hola estado de los dispositivos y supervisar sus actividades.

En caso de un mantenimiento predictivo hello, back-end de soluciones de hello almacena los datos de telemetría históricos. Hola solución back-end puede usar este patrones de tooidentify de toouse de datos que indican un mantenimiento vence en un suministro específico.

Las soluciones de IoT pueden incluir bucles de comentarios automáticos. Por ejemplo, puede identificar un módulo de análisis de back-end de soluciones de Hola de telemetría de temperatura de Hola de un dispositivo específico está por encima de los niveles de funcionamiento normales. solución de Hello, a continuación, puede enviar un dispositivo de toohello comando, dando tootake de acción correctiva.

### <a name="presentation-and-business-connectivity"></a>Presentación y conectividad empresarial

capa de conectividad de presentación y empresarial Hola permite a los usuarios finales toointeract con hello solución de IoT y dispositivos de Hola. Permite a los usuarios tooview y analizar datos de hello recopilados desde sus dispositivos. Estas vistas pueden adoptar forma de Hola de paneles o informes de BI que pueden mostrar tanto datos históricos o cerca de los datos en tiempo real. Por ejemplo, un operador puede comprobar estado de Hola de estación de bombeo determinado y ver todas las alertas por sistema Hola. Este nivel también permite la integración de hello IoT solución back-end con tootie de aplicaciones de línea de negocio existentes en los procesos empresariales o flujos de trabajo. Por ejemplo, hello mantenimiento predictivo solución puede se integra con un sistema de programación que libros un toovisit ingeniero una estación bombeo cuando la solución de hello identifica una bomba necesitan mantenimiento.

![Panel de soluciones de IoT][img-dashboard]

[img-solution-architecture]: ./media/iot-azure-and-iot/iot-reference-architecture.png
[img-dashboard]: ./media/iot-azure-and-iot/iot-suite.png

[lnk-machinelearning]: http://azure.microsoft.com/documentation/services/machine-learning/
[Azure IoT Suite]: http://azure.microsoft.com/solutions/iot
[lnk-protocol-gateway]:  ../articles/iot-hub/iot-hub-protocol-gateway.md
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
