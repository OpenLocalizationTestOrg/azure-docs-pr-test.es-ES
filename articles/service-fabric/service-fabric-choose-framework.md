---
title: "Introducción al modelo de programación aaaService tejido | Documentos de Microsoft"
description: 'Service Fabric ofrece dos marcos para compilar servicios: Hola actor y Hola services framework. Ofrecen distintas ventajas e inconvenientes en simplicidad y control.'
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: vturecek
ms.assetid: 974b2614-014e-4587-a947-28fcef28b382
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: vturecek
ms.openlocfilehash: b48af2a7b41935bdf0e4594c765f363e520c254e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-programming-model-overview"></a>Información general del modelo de programación de Service Fabric
Service Fabric ofrece toowrite de varias maneras y administre sus servicios. Servicios pueden elegir toouse hello las API de tejido de servicio tootake aprovechar características y marcos de aplicaciones de la plataforma de Hola. Los servicios también pueden ser cualquier programa ejecutable compilado escrito en cualquier lenguaje o código que se ejecute en un contenedor hospedado simplemente en un clúster de Service Fabric.

## <a name="guest-executables"></a>Ejecutables de invitado
Un [ejecutable de invitado](service-fabric-deploy-existing-app.md) es un ejecutable arbitrario y existente (escrito en cualquier lenguaje) que se pueda ejecutar como un servicio en la aplicación. Ejecutables de invitado no llame directamente a Hola API del SDK de tejido de servicio. Sin embargo seguir sacando provecho de funciones de la plataforma de hello ofrece, como la detectabilidad del servicio, personalizada del estado y cargar informes mediante una llamada a las API de REST expuesto por Service Fabric. También tienen soporte técnico completo de ciclo de vida de aplicación.

Introducción a los archivos ejecutables de invitado mediante la implementación de la primera [aplicación ejecutable de invitado](service-fabric-deploy-existing-app.md).

## <a name="containers"></a>Contenedores
De forma predeterminada, Service Fabric implementa y activa estos servicios como procesos. Service Fabric puede implementar también servicios en [contenedores](service-fabric-containers-overview.md). Service Fabric admite la implementación de contenedores de Linux y contenedores de Windows en Windows Server 2016. Las imágenes de contenedor pueden extraerse de cualquier repositorio de contenedor e implementan toohello máquina. Puede implementar las aplicaciones existentes como invitado exectuables, servicios confiables de Service Fabric con o sin estado o Reliable Actors de contenedores y pueden mezclar servicios en procesos y servicios en contenedores Hola la misma aplicación.

[más información sobre la inclusión en contenedores de los servicios de Windows o Linux](service-fabric-deploy-container.md)

## <a name="reliable-services"></a>Reliable Services
Servicios de confianza es un marco de ligera para escribir servicios que se integran con la plataforma de Service Fabric hello y aprovechan el conjunto completo de Hola de características de la plataforma. Servicios de confianza proporcionan un conjunto mínimo de las API que permiten Hola Service Fabric en tiempo de ejecución toomanage Hola del ciclo de vida de los servicios y que permiten su toointeract servicios con hello en tiempo de ejecución. marco de aplicación Hello es mínima, ofrecerle completa control sobre las opciones de diseño e implementación, y puede ser usado toohost cualquier otro marco de aplicación, como ASP.NET Core.

Servicios de confianza pueden ser plataformas de servicio toomost sin estado, de forma similar, como los servidores web, en el que cada instancia del servicio de Hola se crea de la misma y se conserva el estado en una solución externa, como base de datos de Azure o almacenamiento de tabla de Azure.

Servicios de confianza también pueden ser con estado, exclusivo tooService tejido, donde se conserva el estado directamente en el servicio de hello utilizando colecciones confiable. El estado cuenta con una alta disponibilidad mediante la replicación y se distribuye a través de particiones, todo administrado automáticamente por Service Fabric.

[Aprenda más sobre Reliable Services](service-fabric-reliable-services-introduction.md) o comience por [escribir su primer Reliable Service](service-fabric-reliable-services-quick-start.md).

## <a name="reliable-actors"></a>Reliable Actors
Se basa en servicios de confianza, framework Actor confiable de hello es un marco de aplicación que implementa el patrón de Actor Virtual hello, basándose en el patrón de diseño de hello actor. marco de Actor confiable de Hello usa unidades independientes del proceso y el estado con la ejecución de un único subproceso denominada actores. Hola Actor confiable framework proporciona comunicaciones predefinidas actores y configuraciones de escalado horizontal y persistencia de estado establecido previamente.

Reliable Actors propio sea el marco de una aplicación basado en los servicios de confianza, está totalmente integrado con la plataforma Service Fabric de Hola y se beneficia del conjunto completo de Hola de características que ofrece la plataforma de Hola.

[Aprenda más sobre Reliable Actors](service-fabric-reliable-actors-introduction.md) o comience por [escribir el primer servicio de Reliable Actor](service-fabric-reliable-actors-get-started.md).

## <a name="aspnet-core"></a>ASP.NET Core
Service Fabric se integra con [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) para compilar servicios web y de API que se pueden incluir como parte de la aplicación. 

[Crear un servicio de front-end mediante ASP.NET Core](service-fabric-add-a-web-frontend.md)

## <a name="next-steps"></a>Pasos siguientes
[Información general sobre Service Fabric y contenedores](service-fabric-containers-overview.md)

[Información general sobre Reliable Services](service-fabric-reliable-services-introduction.md)

[Información general sobre Reliable Services](service-fabric-reliable-actors-introduction.md)

[Service Fabric y ASP.NET Core ](service-fabric-reliable-services-communication-aspnetcore.md)




