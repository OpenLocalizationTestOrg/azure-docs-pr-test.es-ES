---
title: Arquitectura del Administrador de aaaResource | Documentos de Microsoft
description: "Información general de la arquitectura de Service Fabric Cluster Resource Manager"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 6c4421f9-834b-450c-939f-1cb4ff456b9b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9ea80273d0566a2ac25143ada3662875656b57b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-architecture-overview"></a>Información general de la arquitectura del Administrador de recursos de clúster
Hola, Administrador de recursos de clúster de tejido de servicio es un servicio central que se ejecuta en el clúster de Hola. Administra el estado de hello deseado de los servicios de hello en clúster de hello, especialmente con respecto al consumo tooresource y las reglas de selección de ubicación. 

toomanage Hola recursos del clúster, Hola, Administrador de recursos de clúster de tejido de servicio debe tener varias piezas de información:

- Qué servicios existen actualmente
- Consumo de recursos actual (o predeterminado) de cada servicio 
- capacidad de clúster restantes Hola 
- capacidad de Hola de nodos de hello en clúster de Hola 
- cantidad de Hola de los recursos utilizados en cada nodo

consumo de recursos de Hola de un servicio determinado puede cambiar con el tiempo y servicios preocupa normalmente más de un tipo de recurso. En los distintos servicios, es posible que se midan tanto los recursos lógicos como los recursos físicos reales. Los servicios pueden hacer seguimiento de métricas físicas, como el consumo de disco y memoria. Es más frecuentes que los servicios se ocupen de las métricas lógicas, como "WorkQueueDepth" o "TotalRequests". Lógicas y físicas de las métricas pueden utilizarse en hello mismo clúster. Las métricas se pueden compartir entre muchos servicios o ser tooa específico de servicio determinado.

## <a name="other-considerations"></a>Otras consideraciones
Hello propietarios y los operadores de clúster de hello pueden ser diferentes de Hola a los autores de servicio y de aplicación o en un mínimo son Hola mismo personas llevar sombreros distintos. Hay algunas cosas que se saben sobre lo que necesita la aplicación al desarrollarla. Tener una estimación de hello deben implementarse diferentes servicios y recursos que va a consumir. Por ejemplo, nivel de hello web debe toorun en nodos expuestos toohello Internet, mientras los servicios de base de datos de hello no deberían. Como otro ejemplo, servicios web de Hola probablemente están restringidos por la CPU y la red, al cuidado de servicios de nivel de hello datos más información sobre el consumo de memoria y disco. Sin embargo, persona Hola control de un incidente de sitio en vivo para ese servicio en producción, o que está administrando un servicio de actualización toohello tiene un toodo de trabajo diferentes y requiere distintas herramientas. 

Clúster de Hola y servicios son dinámicos:

- puede aumentar y reducir el número de Hola de nodos de clúster de Hola
- Los nodos de distintos tipos y tamaños pueden ir y venir.
- Se pueden crear y quitar servicios, así como cambiarles las asignaciones de recursos y las reglas de selección de ubicación deseadas.
- Las actualizaciones u otras operaciones de administración pueden poner en clúster de hello en la aplicación hello en los niveles de infraestructura
- Pueden generarse errores en cualquier momento.

## <a name="cluster-resource-manager-components-and-data-flow"></a>Componentes y flujo de datos del Administrador de recursos de clúster
Hola, Administrador de recursos del clúster tiene requisitos de Hola de tootrack de cada servicio y Hola el consumo de recursos por cada objeto de servicio dentro de esos servicios. Hola, Administrador de recursos del clúster tiene dos partes conceptuales: agentes que se ejecutan en cada nodo y un servicio de tolerancia. agentes de Hello en cada nodo de la carga de seguimiento informa de los servicios, agregados y periódicamente informa de ellos. Hola servicio Administrador de recursos de clúster agrega toda la información de Hola de agentes locales de Hola y reacciona en función de su configuración actual.

Echemos un vistazo a Hola siguiente diagrama:

<center>
![Arquitectura del equilibrador de recursos][Image1]
</center>

Durante el tiempo de ejecución, pueden ocurrir muchos cambios. Por ejemplo, supongamos que la cantidad de Hola de recursos algunos servicios consumen cambios, algunos errores de servicios, y algunos nodos se conectan y desconectan clúster Hola. Se agregan y se envían periódicamente el servicio de administrador de recursos de clúster de toohello (1,2) donde se agrega de nuevo, analiza y almacena todos los cambios de hello en un nodo. Cada pocos segundos que servicio examina cambios hello y determina si las acciones son necesarias (3). Por ejemplo, podría observar que se han agregado algunos nodos vacíos toohello clúster. Como resultado, decisión toomove algunos nodos de toothose de servicios. Hello Administrador de recursos del clúster podría también tenga en cuenta que un nodo concreto está sobrecargado o que determinados servicios se error o se ha eliminado, lo que libera recursos en otra parte.

Vamos a mirar Hola después de diagrama y vea Qué sucede a continuación. Vamos a decir que Hola, Administrador de recursos del clúster determina que son necesarios cambios. Coordina con otros cambios necesarios del sistema servicios (Hola determinado el Administrador de conmutación por error) toomake Hola. A continuación, los comandos necesarios de Hola se envían nodos correspondientes toohello (4). Por ejemplo, supongamos que Hola, Administrador de recursos había observado que Nodo5 sobrecarga y, por lo que decidió toomove servicio B de tooNode4 Nodo5. Al final de Hola de reconfiguración de hello (5), el clúster de hello tiene este aspecto:

<center>
![Arquitectura del equilibrador de recursos][Image2]
</center>

## <a name="next-steps"></a>Pasos siguientes
- Hola, Administrador de recursos del clúster tiene muchas opciones para describir el clúster de Hola. toofind más información acerca de ellos, consulte este artículo en [que describe un clúster de Service Fabric](./service-fabric-cluster-resource-manager-cluster-description.md)
- tareas principal del Administrador de recursos de clúster Hola son reequilibrio clúster hello y exigir reglas de selección de ubicación. Para más información sobre cómo configurar estos comportamientos, vea [Equilibrio del clúster de Service Fabric](./service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-1.png
[Image2]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-2.png
