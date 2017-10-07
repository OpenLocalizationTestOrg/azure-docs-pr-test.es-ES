---
title: aaaOverview de AMQP 1.0 Service Bus de Azure | Documentos de Microsoft
description: "Obtenga información acerca del uso de Hola Advanced Message Queuing Protocol (AMQP) 1.0 en Azure."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0e8d19cc-de36-478e-84ae-e089bbc2d515
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: c35a20c50dd24845d9a4c7a0251e8240848a6f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-support-in-service-bus"></a>Soporte de AMQP 1.0 en el Bus de servicio
Ambos Hola servicio Service Bus de Azure en la nube y locales [Service Bus para Windows Server (Service Bus 1.1)](https://msdn.microsoft.com/library/dn282144.aspx) soporte Hola Advanced Message Queueing Protocol (AMQP) 1.0. AMQP permite toobuild entre plataformas, aplicaciones híbridas con un protocolo estándar abierto. Puede construir aplicaciones mediante componentes creados con distintos lenguajes y marcos, y que se ejecutan en diferentes sistemas operativos. Todos estos componentes pueden conectarse tooService Bus y perfectamente intercambien mensajes empresariales estructurados con total fidelidad y eficazmente.

## <a name="introduction-what-is-amqp-10-and-why-is-it-important"></a>Introducción: ¿Qué es AMQP 1.0 y por qué es tan importante?
Tradicionalmente, los productos de middleware orientados a mensajes utilizaban protocolos propietarios para la comunicación entre las aplicaciones cliente y los agentes. Esto significa que una vez que haya seleccionado de agente de mensajería de un proveedor determinado, debe utilizar tooconnect de bibliotecas de ese proveedor el broker de toothat de las aplicaciones de cliente. Esto permite un grado de dependencia de ese proveedor, ya que trasladar un producto diferente de tooa de aplicación requiere cambios de código en todas las aplicaciones de hello conectado. 

Además, es difícil conectar a los agentes de mensajes de diferentes proveedores. Normalmente esto requiere mensajes de toomove protocolo de puente de nivel de aplicación de un sistema tooanother y tootranslate entre sus formatos de mensaje propietario. Se trata de un requisito común; Por ejemplo, cuando debe proporcionar un nuevo tooolder interfaz unificada sistemas dispares o integrar los sistemas de TI después de una fusión.

industria del software Hola trata de una empresa movimientos rápidos; se introducen nuevos lenguajes de programación y marcos de aplicaciones a un ritmo a veces desconcertante. De forma similar, evolucionan los requisitos de Hola de sistemas de TI y desarrolladores quieren tootake aprovechar las características más recientes de la plataforma de Hola. Sin embargo, a veces hello proveedor mensajería seleccionado no admite estas plataformas. Dado que los protocolos de mensajería son propietarios, no es posible para otros tooprovide bibliotecas estas nuevas plataformas. Por lo tanto, debe usar métodos como crear puertas de enlace o puentes que le permiten producto de mensajería toocontinue toouse Hola.

desarrollo de Hola de hello Advanced Message Queuing Protocol (AMQP) 1.0 estuvo motivado por estos problemas. Tuvo su origen en JP Morgan Chase, que, al igual que la mayoría de empresas de servicios financieros, consume una gran cantidad de middleware orientado a mensajes. objetivo de Hello fue simple: toocreate un protocolo de mensajería estándar abierto que se realiza utilizando componentes creados con distintos lenguajes, marcos y sistemas operativos, las aplicaciones basadas en mensajes toobuild posibles todos utilicen componentes de las mejores desde un intervalo de proveedores.

## <a name="amqp-10-technical-features"></a>Características técnicas de AMQP 1.0
AMQP 1.0 es un protocolo de mensajería eficaz, confiable y el nivel de conexión que se pueden usar toobuild sólida entre plataformas, aplicaciones de mensajería. Protocolo de Hello tiene un objetivo simple: mecanismos de hello toodefine de transferencia segura, confiable y eficaz de Hola de mensajes entre dos entidades. Hola mensajes se codifican utilizando una representación de datos portátiles que permite heterogéneos mensajes de negocio de la tooexchange estructurado remitentes y receptores con total fidelidad. Hola te mostramos un resumen de las características más importantes de hello:

* **Eficaz**: AMQP 1.0 es un protocolo orientado a la conexión que utiliza una codificación para hello binaria instrucciones de protocolo y Hola mensajes empresariales transferidos con él. Incorpora la utilización de sofisticadas de control de flujo esquemas toomaximize Hola de red de Hola y los componentes de hello conectado. Es decir, el protocolo de hello era toostrike diseñado un equilibrio entre la eficacia, la flexibilidad y la interoperabilidad.
* **Confiable**: Hola protocolo AMQP 1.0 permite toobe de mensajes intercambiado con un intervalo de garantías de confiabilidad, desde enviar y olvidarse tooreliable, exactamente-una vez confirmado la entrega.
* **Flexible**: AMQP 1.0 es un protocolo flexible que puede ser usado toosupport diferentes topologías. Hello mismo protocolo se puede utilizar para las comunicaciones de cliente a cliente, el agente de cliente y agente a agente.
* **Independiente del modelo de agente**: Hola especificación AMQP 1.0 no impone ningún requisito en el modelo de mensajería de hello utilizado por un agente. Esto significa que es posible tooeasily agregar tooexisting de compatibilidad con AMQP 1.0 corredores de bolsa de mensajería.

## <a name="amqp-10-is-a-standard-with-a-capital-s"></a>AMQP 1.0 es un Estándar (con mayúscula)
AMQP 1.0 es un estándar internacional, aprobado por ISO e IEC como ISO/IEC 19464:2014.

AMQP 1.0 lo ha estado desarrollando desde 2008 un grupo central de 20 compañías, tanto proveedores de tecnología como empresas usuarias. Durante ese tiempo, empresas de usuarios han contribuido a sus requisitos empresariales reales y los proveedores de tecnología de hello han evolucionado Hola protocolo toomeet esos requisitos. Durante el proceso de hello, los proveedores han participado en talleres en el que han colaborado interoperabilidad de hello toovalidate entre sus implementaciones.

En octubre de 2011, el trabajo de desarrollo Hola pasado tooa Comité técnico dentro de hello organización para Advancement of Structured información Standards (OASIS) Hola y Hola estándar OASIS AMQP 1.0 se publicó en octubre de 2012. Hello siguientes empresas participaron en Comité técnico de Hola durante el desarrollo de Hola de hello estándar:

* **Proveedores de tecnología**: Axway Software, Huawei Technologies, IIT Software, INETCO Systems, Kaazing, Microsoft, Mitre Corporation, Primeton Technologies, Progress Software, Red Hat, SITA, Software AG, Solace Systems, VMware, WSO2, Zenika.
* **Firmas de usuario**: Bank of America, Credit Suisse, Deutsche Boerse, Goldman Sachs, JPMorgan Chase.

Algunos de hello citaron normalmente son algunas ventajas de estándares abiertos:

* Menos probabilidad de dependencia con el proveedor
* Interoperabilidad
* Amplia disponibilidad de bibliotecas y herramientas
* Protección contra la obsolescencia
* Disponibilidad de personal experto
* Menor riesgo y más controlable

## <a name="amqp-10-and-service-bus"></a>AMQP 1.0 y Bus de servicio
Compatibilidad con AMQP 1.0 Service Bus de Azure significa que ahora pueden aprovechar la cola de Bus de servicio de Hola y publicación/suscripción características de mensajería asíncrona entre una gama de plataformas, mediante un eficaz protocolo binario. Además, puede desarrollar aplicaciones formadas por componentes creados con una mezcla de lenguajes, marcos y sistemas operativos.

Hello en la ilustración siguiente se muestra una implementación de ejemplo en las que los clientes de Java que se ejecutan en Linux, escritos con la API de Java Message Service (JMS) estándar de Hola y los clientes de .NET que se ejecutan en Windows, intercambian mensajes a través del Bus de servicio con AMQP 1.0.

![][0]

**Figura 1: Escenario de implementación de ejemplos que muestran mensajes entre plataformas mediante Service Bus y AMQP 1.0**

En este Hola de tiempo siguientes bibliotecas de cliente se conocen toowork con Bus de servicio:

| language | Biblioteca |
| --- | --- |
| Java |Cliente de Java Message Service (JMS) Apache Qpid<br/>Cliente de Java SwiftMQ, de IIT Software. |
| C |Apache Qpid Proton-C |
| PHP |Apache Qpid Proton-PHP |
| Python |Apache Qpid Proton-Python |
| C# |AMQP .Net Lite |

**Figura 2: Tabla de bibliotecas de cliente de AMQP 1.0**

## <a name="summary"></a>Resumen
* AMQP 1.0 es un protocolo de mensajería confiable y abierto que puede utilizar aplicaciones híbridas de toobuild multiplataforma. AMQP 1.0 es un estándar de OASIS.
* La compatibilidad con AMQP 1.0 ahora está disponible en el Bus de servicio de Azure, así como en el Bus de servicio para Windows Server (Bus de servicio 1.1). El precio es igual que para Hola existente protocolos de Hola.

## <a name="next-steps"></a>Pasos siguientes
¿Toolearn listo más? Visite Hola siguientes vínculos:

* [Uso de Service Bus desde .NET con AMQP]
* [Uso de Service Bus desde Java con AMQP]
* [Instalación de Apache Qpid Proton-C en una VM Linux de Azure]
* [AMQP de Service Bus para Windows Server]

[0]: ./media/service-bus-amqp-overview/service-bus-amqp-1.png
[Uso de Service Bus desde .NET con AMQP]: service-bus-amqp-dotnet.md
[Uso de Service Bus desde Java con AMQP]: service-bus-amqp-java.md
[Instalación de Apache Qpid Proton-C en una VM Linux de Azure]: service-bus-amqp-apache.md
[AMQP de Service Bus para Windows Server]: https://msdn.microsoft.com/library/dn574799.aspx
