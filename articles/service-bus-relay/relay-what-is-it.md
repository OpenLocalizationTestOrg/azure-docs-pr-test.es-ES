---
title: "aaaWhat retransmisión de Azure y por qué usarla Introducción | Documentos de Microsoft"
description: "Información general sobre Relay de Azure"
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1e3e971d-2a24-4f96-a88a-ce3ea2b1a1cd
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 4cfd77048210a435c446b908b7896737cad0edbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-relay"></a>¿Qué es Relay de Azure?

Hola retransmisión Azure servicio facilita híbrida aplicaciones habilitando toosecurely exponen los servicios que residen dentro de una nube pública de la toohello de red empresas corporativas, sin necesidad de tooopen una conexión de servidor de seguridad, o requieran intrusivo cambia tooa infraestructura de red corporativa. Relay admite diversos protocolos de transporte y estándares de servicios web.

servicio de retransmisión de Hello admite tradicional de solicitud/respuesta unidireccional y el tráfico de punto a punto. También admite la distribución de eventos en escenarios de publicación/suscripción tooenable de ámbito de internet y la comunicación de socket bidireccional para conseguir una eficacia mayor punto a punto. 

En patrón de transferencia de datos de hello retransmitida, un servicio local conecta toohello servicio de retransmisión a través de un puerto de salida y crea un socket bidireccional para la dirección de comunicación enlazada tooa encuentro concreta. cliente de Hello, a continuación, puede comunicarse con servicio local de hello mediante el envío de servicio de retransmisión de tráfico toohello Hola rendezvous dirección de destino. servicio de retransmisión de Hello, a continuación, "retransmite" servicio de datos toohello local a través de un cliente de socket bidireccional tooeach dedicado. Hello cliente no necesita un conexión directa toohello servicio de forma local, no es necesario tooknow donde reside el servicio de Hola y Hola local servicio no necesita ningún puerto de entrada abierto en firewall de Hola.

los elementos de capacidad clave Hola proporcionados por retransmisión son comunicación bidireccional, no almacenado en búfer en los límites de red con la limitación similares a TCP, detección de punto de conexión, estado de conectividad y superponer seguridad del punto final. capacidades de retransmisión de Hello difieren de las tecnologías de integración en el nivel de red como VPN, en dicha retransmisión puede ser extremo de la aplicación solo de tooa con ámbito en un único equipo, mientras que la tecnología VPN es mucho más intrusiva tal y como se basa en modificar el entorno de red de Hola .

Relay de Azure tiene dos características:

1. [Las conexiones híbridas](#hybrid-connections) : sockets de usos hello web estándar abierto que permite escenarios multiplataformas.
2. [Retransmisiones de WCF](#wcf-relays) -llamadas a procedimiento remoto tooenable usa Windows Communication Foundation (WCF). Retransmisión de WCF es retransmisión heredado Hola oferta que ya utilicen muchos clientes con su modelos de programación de WCF.

Las conexiones híbridas y retransmisiones de WCF permiten tooassets de conexión segura que existen dentro de una red de empresas corporativas. Uso de una frente a Hola otro es depende de sus necesidades concretas, como se describe en hello en la tabla siguiente:

|  | Retransmisión de WCF | conexiones híbridas |
| --- |:---:|:---:|
| **WCF** |x | |
| **.NET Core** | |x |
| **.NET Framework** |x |x |
| **JavaScript/NodeJS** | |x |
| **Protocolo abierto basado en estándares** | |x |
| **Varios modelos de programación de RPC** | |x |

## <a name="hybrid-connections"></a>conexiones híbridas

Hola [conexiones híbridas de Azure retransmisión](relay-hybrid-connections-protocol.md) capacidad es una evolución segura, protocolo abierto de hello las funciones de retransmisión que se pueden implementar en cualquier plataforma y en cualquier lenguaje que tiene una capacidad de WebSocket básica existentes que incluya explícitamente hello WebSocket API en exploradores web más habituales. Conexiones híbridas se basa en HTTP y WebSockets.

### <a name="service-history"></a>Historial de servicios

Las conexiones híbridas suplanta primero hello, característica de "Servicios de BizTalk" que se compiló Hola retransmisión de WCF de Bus de servicio de Azure de forma similar a la llamada. nueva funcionalidad de las conexiones híbridas Hola complementa la característica de retransmisión de WCF existente de Hola y estas capacidades de dos servicios existen en paralelo en el servicio de retransmisión de Azure Hola. Aunque comparten una puerta de enlace común, se trata de implementaciones diferentes.

## <a name="wcf-relays"></a>Relés de WCF

Hola funciona de retransmisión de WCF para Hola completa .NET Framework (NETFX) y de WCF. Iniciar conexión Hola entre el servicio local y servicio de retransmisión de hello mediante un conjunto de enlaces de WCF "de retransmisión". Entre bastidores de hello, enlaces de retransmisión de hello asignan toonew transporte enlace elementos diseñados toocreate WCF componentes de canal que se integran con el Bus de servicio en nube de Hola.

## <a name="architecture-processing-of-incoming-relay-requests"></a>Arquitectura: Procesamiento de solicitudes entrantes de retransmisión
Cuando un cliente envía una solicitud toohello [Azure retransmisión](/azure/service-bus-relay/) servicio, el equilibrador de carga de Azure Hola lo enruta tooany de nodos de la puerta de enlace de Hola. Si la solicitud de hello es una solicitud de escucha, nodo de puerta de enlace de hello crea una nueva retransmisión. Si la solicitud de hello es una retransmisión específicos de tooa de solicitud de conexión, nodo de puerta de enlace de hello reenvía Hola conexión solicitud toohello puerta de enlace nodo que posee la retransmisión de Hola. nodo de puerta de enlace de Hola que posee la retransmisión de hello envía un rendezvous solicitud toohello escucha cliente, pedir toocreate de agente de escucha de hello en un nodo de puerta de enlace de canal temporal toohello que recibió una solicitud de conexión de Hola.

Cuando se establece la conexión de retransmisión de hello, los clientes de hello pueden intercambiar mensajes a través del nodo de puerta de enlace de Hola que se utiliza para rendezvous Hola.

![Procesamiento de solicitudes entrantes de retransmisión WCF](./media/relay-what-is-it/ic690645.png)

## <a name="next-steps"></a>Pasos siguientes

* [Preguntas más frecuentes acerca de Relay](relay-faq.md)
* [Creación de un espacio de nombres](relay-create-namespace-portal.md)
* [Introducción a .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introducción a Node](relay-hybrid-connections-node-get-started.md)

