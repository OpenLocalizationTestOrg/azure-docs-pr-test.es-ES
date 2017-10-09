---
title: "Instancias de contenedor de aaaAzure y orquestación de contenedor"
description: "Descripción de cómo Azure Container Instances interactúa con orquestadores de contenedores"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a>Azure Container Instances y orquestadores de contenedores

Los contenedores, debido a su tamaño pequeño y a la orientación de aplicaciones, se adaptan perfectamente a entornos de entrega ágil y arquitecturas basadas en microservicios. tarea de Hello de automatizar y administrar un gran número de contenedores y cómo interactúan se conoce como *orquestación*. Orchestrators contenedor populares incluyen Kubernetes, DC/OS y Docker Swarm, todas ellas están disponibles en hello [servicio de contenedor de Azure](https://docs.microsoft.com/azure/container-service/).

Instancias de contenedor de Azure proporciona algunas hello básico de funcionalidades de plataformas de orquestación de programación, pero no se tratan los servicios de valor más alto de Hola que esas plataformas proporcionan y de hecho pueden ser complementarias con ellos. Este artículo describe el ámbito de Hola de lo que controla las instancias de contenedor de Azure y cuánto orchestrators contenedor podrían interactuar con él.

## <a name="traditional-orchestration"></a>Orquestación tradicional

definición estándar de Hola de orquestación incluye Hola siguientes tareas:

- **Programación**: debido a una imagen de contenedor y una solicitud de recursos, encontrar una máquina adecuada en qué contenedor de hello toorun.
- **Afinidad/antiafinidad**: especifique que un conjunto de contenedores se deben ejecutar de manera cercana entre sí (para mejorar el rendimiento) o con la distancia suficiente como para mejorar la disponibilidad.
- **Seguimiento de estado**: inspeccione los contenedores por si existen errores y vuelva a programarlos.
- **Conmutación por error**: realizar un seguimiento de lo que se ejecuta en cada equipo y volver a programar los contenedores de los nodos de toohealthy de equipos con errores.
- **Ajuste de escala**: agregar o quitar la petición de toomatch de instancias de contenedor, ya sea de forma manual o automática.
- **Redes**: proporcione una red superpuesta para coordinar todas las toocommunicate de contenedores en varios equipos host.
- **Detección de servicios**: habilitar contenedores toolocate entre sí automáticamente incluso cuando pasan entre equipos host y cambiar las direcciones IP.
- **Coordina las actualizaciones de aplicaciones**: administrar aplicación tooavoid las actualizaciones de contenedor de tiempo de inactividad y habilitar la reversión si algo va mal.

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a>Orquestación con Azure Container Instances: un enfoque por niveles

Instancias de contenedor de Azure permite un tooorchestration enfoque por capas, que ofrece toda la programación de Hola y capacidades de administración necesario toorun un único contenedor, permitiendo orchestrator tareas de contenedor múltiples plataformas toomanage sobre él.

Porque todos Hola infraestructura subyacente para instancias de contenedor está administrado por Azure, una plataforma de orchestrator no es necesario tooconcern con la búsqueda de una máquina de host correspondiente en qué toorun un único contenedor. elasticidad de Hola de nube de hello garantiza que uno siempre esté disponible. En su lugar, orchestrator Hola puede centrarse en tareas de Hola que simplifican el desarrollo de Hola de contenedor varias arquitecturas, incluido el ajuste y coordina las actualizaciones.



## <a name="potential-scenarios"></a>Escenarios potenciales

Si bien la integración de los orquestadores con Azure Container Instances todavía es incipiente, podemos prever que surgirán algunos entornos distintos:

### <a name="orchestration-of-container-instances-exclusively"></a>Orquestación exclusiva de Container Instances

Dado que se inician rápidamente y facturar por hello segundo, un entorno basado exclusivamente en instancias de contenedor de Azure ofrece inició tooget de manera más rápida de Hola y toodeal con cargas de trabajo muy variables.

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a>Combinación de Container Instances y contenedores en máquinas virtuales

De ejecución prolongada, cargas de trabajo estables, orquestar contenedores en un clúster de máquinas virtuales dedicadas suele ser más económico que ejecuta Hola mismos contenedores con instancias de contenedor. Sin embargo, las instancias de contenedor ofrecen una excelente solución para rápidamente expandir y contraer los toodeal de capacidad total con picos inesperados o de corta duración en el uso. En lugar de escalado horizontal de número de Hola de máquinas virtuales en el clúster, a continuación, implementar contenedores adicionales en dichos equipos, Hola orchestrator puede simplemente programar contenedores adicionales de hello mediante instancias de contenedor y eliminarlos cuando están sin es necesario.

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a>Implementación de ejemplo: conector de Azure Container Instances para Kubernetes

toodemonstrate cómo pueden integrar las plataformas de orquestación de contenedor con instancias de contenedor de Azure, hemos hemos iniciado la creación una [conector de ejemplo para Kubernetes][aci-connector-k8s]. 

Hola conector para Kubernetes imita hello [kubelet] [ kubelet-doc] mediante el registro como un nodo con una capacidad ilimitada y enviar la creación de hello de [pod] [ pod-doc] como grupos del contenedor en instancias de contenedor de Azure. 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

Pudieron crear conectores para otras orchestrators, del mismo modo integrado con alimentación de plataforma primitivas toocombine Hola de orchestrator Hola API con una velocidad de Hola y la simplicidad de la administración de contenedores en instancias de contenedor de Azure.

> [!WARNING]
> Hola conector ACI para Kubernetes es *experimental* y no debe usarse en producción.

## <a name="next-steps"></a>Pasos siguientes

Crear el primer contenedor con instancias de contenedor de Azure mediante hello [Guía de inicio rápido](container-instances-quickstart.md).

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/