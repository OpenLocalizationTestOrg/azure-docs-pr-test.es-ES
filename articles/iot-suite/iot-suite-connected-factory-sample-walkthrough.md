---
title: "Tutorial de la solución de aaaConnected generador Suite de IoT de Azure | Documentos de Microsoft"
description: "Una descripción de solución de IoT de Azure preconfigurado hello conectados generador y su arquitectura."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a>Tutorial de la solución de fábrica preconfigurada conectada

Hola IoT Suite conectado generador [preconfigurado solución] [ lnk-preconfigured-solutions] es una implementación de una solución industrial-to-end que:

* Se conecta tooboth simulada dispositivos industrial ejecutan servidores de OPC UA en líneas de producción de fábrica simulada y dispositivos de servidor de OPC UA reales. Para obtener más información sobre OPC UA, vea hello [conectado generador preguntas más frecuentes sobre](iot-suite-faq-cf.md).
* Muestra las claves KPI operativas y el OEE de esos servicios y líneas de producción.
* Muestra cómo una aplicación basada en la nube podría ser toointeract usado con sistemas de servidor de OPC UA.
* Permite tooconnect sus propios dispositivos de servidor de OPC UA.
* Le permite toobrowse y modificar datos del servidor de OPC UA Hola.
* Se integra con hello tooprovide de servicio de información de serie de tiempo de Azure (ETI) vistas personalizadas de datos de saludo de los servidores de OPC UA.

Puede usar soluciones de hello como punto de partida para su propia implementación y [personalizar] [ lnk-customize] toomeet sus propios requisitos empresariales específicos.

Este artículo le guiará a través de algunos de los elementos clave de Hola de hello conectado generador solución tooenable toounderstand su funcionamiento. Esta información le ayuda a:

* Solucionar problemas de solución de Hola.
* Planear cómo toocustomize toohello solución toomeet sus propios requisitos específicos.
* Diseñar una solución de IoT propia que utilice servicios de Azure.

Para obtener más información, vea hello [conectado generador preguntas más frecuentes sobre](iot-suite-faq-cf.md).

## <a name="logical-architecture"></a>Arquitectura lógica

Hola siguiente diagrama describe los componentes lógicos de Hola de solución de hello preconfigurado:

![Arquitectura lógica de fábrica conectada][connected-factory-logical]

## <a name="communication-patterns"></a>Patrones de comunicación

solución de Hello usa hello [especificación de OPC UA Pub/Sub](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend tooIoT de datos de telemetría OPC UA concentrador en formato JSON. solución de Hello usa hello [OPC publicador](https://github.com/Azure/iot-edge-opc-publisher) módulo IoT Edge para este propósito.

solución de Hello también tiene un cliente de OPC UA integrado en una aplicación web que puede establecer conexiones con servidores de agente de usuario de OPC locales. Hola cliente utiliza un [proxy inverso](https://wikipedia.org/wiki/Reverse_proxy) y recibe ayuda de conexión de centro de IoT toomake Hola sin necesidad de abrir los puertos en firewall de hello en local. Este patrón de comunicación se denomina [comunicación asistida por el servicio](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/). solución de Hello usa hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) módulo IoT Edge para este propósito.


## <a name="simulation"></a>Simulation

Hola simula las estaciones y la ejecución de fabricación de hello simulado sistemas (MES) constituyen una línea de producción de fábrica. Hello hello OPC publicador módulo y dispositivos simulados se basan en hello [OPC UA .NET estándar] [ lnk-OPC-UA-NET-Standard] publicados por hello Foundation de OPC.

Hello OPC Proxy y el publicador de OPC se implementan como módulos basados en [Azure IoT borde][lnk-Azure-IoT-Gateway]. Cada línea de producción simulada tiene asociada una puerta de enlace designada.

Todos los componentes de simulación se ejecutan en contenedores de Docker hospedados en una máquina virtual Linux de Azure. simulación de Hello es ocho líneas de producción configurado toorun simulada de forma predeterminada.

## <a name="simulated-production-line"></a>Línea de producción simulada

Una línea de producción fabrica piezas. La forman distintas estaciones: una estación de ensamblado, una estación de prueba y una estación de empaquetado.

simulación de Hola se ejecuta y actualiza los datos de Hola que se exponen a través de nodos de agente de usuario de OPC Hola. Hola MES a través de OPC UA se organizan todas las estaciones de la línea de producción simulada.

## <a name="simulated-manufacturing-execution-system"></a>Sistema de ejecución de fabricación simulado

Hola MES supervisa cada estación en la línea de producción de hello con cambios de estado de OPC UA toodetect estación. Llama a OPC UA estaciones de métodos toocontrol hello y pasa a continuación un producto de una estación toohello hasta que se complete.

## <a name="gateway-opc-publisher-module"></a>Módulo publicador de OPC de puerta de enlace

Módulo de publicador de OPC se conecta a servidores de agente de usuario de OPC estación toohello y se suscribe toohello OPC nodos toobe publicado. módulo de Hello convierte los datos del nodo hello en formato JSON, lo cifra y envía tooIoT concentrador como mensajes de agente de usuario de OPC Pub/Sub.

módulo de OPC publicador Hola solo requiere un puerto de salida https (443) y puede trabajar con la infraestructura empresarial existente.

## <a name="gateway-opc-proxy-module"></a>Módulo proxy de OPC de puerta de enlace

Hola módulo de Proxy de agente de usuario de puerta de enlace de OPC túneles mensajes de comando y control de OPC UA binarios y solo requiere un puerto de salida https (443). Puede funcionar con la infraestructura empresarial existente, incluidos los proxies web.

Usa datos de dispositivos del centro de IoT métodos tootransfer qué TCP/IP en el nivel de aplicación Hola y, por tanto, se asegura de confianza de punto de conexión, el cifrado de datos y la integridad mediante el uso de SSL/TLS.

Hola protocolo binario de OPC UA retransmitida a través de proxy de hello propio usa cifrado y la autenticación de agente de usuario.

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

Hola módulo de publicador de puerta de enlace de OPC suscribe cambios tooOPC UA server nodos toodetect hello en valores de datos. Si se detecta un cambio de datos en uno de los nodos de hello, este módulo, a continuación, envía mensajes tooAzure centro de IoT.

Centro de IoT proporciona un tooAzure de origen de evento ETI. Los datos de almacenes de ETI durante 30 días en función de las marcas de tiempo adjuntar toohello mensajes. Estos datos incluyen:

* OPC UA ApplicationUri
* OPC UA NodeId
* Valor del nodo de Hola
* Marca de tiempo de origen
* OPC UA DisplayName

Actualmente, ETI no permite que los clientes toocustomize cuánto hubieran querido tookeep datos de Hola para.

TSI realiza consultas en los datos del nodo mediante SearchSpan (Time.From, Time.To) y los agrega mediante OPC UA ApplicationUri, OPC UA NodeId u OPC UA DisplayName.

datos de Hola de tooretrieve para medidores OEE y KPI de Hola y líneas de serie del tiempo de hello, los datos se agregan por recuento de eventos, Sum, Avg, Min y Max.

serie temporal de Hola se compila con un proceso diferente. OEE y KPI se calcula a partir de datos de base de estación y propaga hacia arriba para la topología de hello (líneas de producción, generadores, enterprise) en la aplicación hello.

Además, serie temporal para la topología OEE y un KPI se calcula en la aplicación hello, cada vez que un objeto timespan mostrado esté listo. Por ejemplo, vista de día de Hola se actualiza cada hora completa.

vista en Hello tiempo series de datos del nodo proviene directamente de ETI utilizando una agregación de intervalo de tiempo.

## <a name="iot-hub"></a>IoT Hub
Hola [centro de IoT] [ lnk-IoT Hub] recibe los datos enviados desde Hola OPC publicador módulo en la nube de Hola y facilita el servicio de Azure ETI toohello disponible. 

Hola centro de IoT de solución de hello también:
- Mantiene un registro de la identidad que almacena los identificadores de Hola para todos los OPC publicador módulo y todos los módulos de Proxy de OPC.
- Se utiliza como canal de transporte para la comunicación bidireccional de hello módulo de Proxy de OPC.

## <a name="azure-storage"></a>Azure Storage
solución de Hello utiliza almacenamiento de blobs de Azure como almacenamiento en disco para datos de implementación de VM y toostore Hola.

## <a name="web-app"></a>Aplicación web
aplicación web de Hello implementada como parte de la solución de hello preconfigurado está formado por un cliente de OPC UA integrado, el procesamiento de alertas y la visualización de telemetría.

## <a name="next-steps"></a>Pasos siguientes

Puede seguir introducción con Suite IoT leyendo Hola siguientes artículos:

* [Permisos en el sitio de hello azureiotsuite.com][lnk-permissions]
* [Implementar una puerta de enlace de Windows o Linux para la solución de fábrica preconfigurado Hola conectado](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
