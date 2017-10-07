---
title: aaaIntroduction tooAzure servicio de contenedor para Kubernetes | Documentos de Microsoft
description: Servicio de contenedor de Azure para Kubernetes resulta sencillo toodeploy y administrar aplicaciones basadas en el contenedor en Azure.
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Kubernetes, Docker, Containers, microservicios, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a>Introducción tooAzure servicio de contenedor para Kubernetes
Servicio de contenedor de Azure para Kubernetes resulta sencillo toocreate, configurar y administrar un clúster de máquinas virtuales que forman las aplicaciones preconfiguradas toorun en contenedores. Esto permite toouse sus conocimientos, o dibujar en un cuerpo elevado y creciente de conocimientos de la Comunidad, toodeploy y administrar aplicaciones basadas en el contenedor en Microsoft Azure.

Mediante el servicio de contenedor de Azure, puede aprovechar las ventajas del programa Hola a características de nivel empresarial de Azure, manteniendo la portabilidad de aplicación a través de Kubernetes y Hola formato de imagen de Docker.

## <a name="using-azure-container-service-for-kubernetes"></a>Uso de Azure Container Service para Kubernetes
Nuestro objetivo con el servicio de contenedor de Azure es tooprovide un entorno de hospedaje de contenedor mediante el uso de herramientas de código abierto y tecnologías que son populares entre los clientes hoy en día. toothis final, se exponen los puntos de conexión de la API de Kubernetes estándar Hola. Mediante el uso de estos puntos de conexión estándar, puede aprovechar cualquier software que es capaz de comunicarse tooa Kubernetes clúster. Por ejemplo, puede elegir [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) o [draft](https://github.com/Azure/draft).

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a>Creación de un clúster de Docker mediante Azure Container Service
toobegin con el servicio de contenedor de Azure, implementar un clúster de servicio de contenedor de Azure con hello [CLI de Azure 2.0](container-service-kubernetes-walkthrough.md) o a través del portal de hello (Hola búsqueda Marketplace para **servicio de contenedor de Azure**). Si es un usuario avanzado que necesita más control sobre las plantillas de Azure Resource Manager de hello, puede usar código abierto de hello [motor acs](https://github.com/Azure/acs-engine) proyecto toobuild sus propio Kubernetes personalizados de clúster e implementarla a través de Hola `az` CLI.

### <a name="using-kubernetes"></a>Uso de Kubernetes
Kubernetes automatiza la implementación, el escalado y la administración de aplicaciones en contenedor. Tiene un amplio conjunto de características que incluyen:
* Empaquetamiento automático en contenedores
* Recuperación automática
* Escalado horizontal
* Detección de servicio y equilibrio de carga
* Lanzamientos y reversiones automatizados
* Administración de configuración y secretos
* Orquestación de almacenamiento
* Ejecución por lotes

Diagrama de la arquitectura de Kubernetes implementado a través de Azure Container Service:

![Servicio de contenedor de Azure había configurado toouse Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a>Vídeos

Compatibilidad con Kubernetes de Azure Container Services (Azure, viernes, enero de 2017):

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

Herramientas para desarrollar e implementar aplicaciones en Kubernetes (Azure OpenDev, junio de 2017):

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a>Pasos siguientes

Explorar hello [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin explorar el servicio de contenedor de Azure hoy en día.
