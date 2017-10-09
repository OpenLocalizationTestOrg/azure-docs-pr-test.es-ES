---
title: grupos de agente de aaaDC/OS para el servicio de contenedor de Azure | Documentos de Microsoft
description: "Cómo funcionan los grupos de hello agente públicas y privadas con un clúster de servicio de contenedor de Azure DC/OS"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a>Grupos de agentes de DC/OS para Azure Container Service
Los clústeres de DC/OS en Azure Container Service contienen nodos de agente en dos grupos, uno público y otro privado. Se puede implementar una aplicación de grupo de tooeither, afectar a su accesibilidad entre máquinas en el servicio de contenedor. Hello máquinas pueden estar expuesto toohello internet (público) o mantienen interno (privado). En este artículo se ofrece una breve descripción de por qué hay grupos públicos y privados.


* **Agentes privados**: los nodos de agentes privados se ejecutan mediante una red no enrutable. Esta red solo es accesible desde la zona de administración de Hola o a través de enrutador perimetral de hello zona pública. De forma predeterminada, DC/OS inicia aplicaciones en nodos de agente privado. 

* **Agentes públicos**: los nodos de agentes públicos ejecutan servicios y aplicaciones de DC/OS por medio de una red de acceso público. 

Para obtener más información acerca de la seguridad de red del controlador de dominio/OS, vea hello [documentación del controlador de dominio/OS](https://dcos.io/docs/1.7/administration/securing-your-cluster/).

## <a name="deploy-agent-pools"></a>Implementación de grupos de agentes

Hola DC/OS agente grupos en el servicio de contenedor de Azure se crean como sigue:

* Hola **grupo privada** contiene Hola número de nodos de agente que especifique cuándo se [implementar Hola DC/OS clúster](container-service-deployment.md). 

* Hola **grupo público** inicialmente contiene un número predeterminado de nodos de agente. Este grupo se agrega automáticamente cuando se aprovisionan clústeres de Hola DC/OS.

Hola privada grupo y Hola públicos son conjuntos de escalas de máquina virtual de Azure. Puede cambiar el tamaño de estos grupos después de la implementación.

## <a name="use-agent-pools"></a>Uso de grupos de agentes
De forma predeterminada, **maratón** implementa cualquier toohello de aplicación nueva *privada* nodos de agente. Tener tooexplicitly implementar Hola aplicación toohello *público* nodos durante la creación de hello de aplicación hello. Seleccione hello **opcional** pestaña y escriba **slave_public** para hello **aceptado recursos Roles** valor. Este proceso está documentado [aquí](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) y Hola [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentación.

## <a name="next-steps"></a>Pasos siguientes
* Lea sobre cómo [administrar los contenedores de DC/OS](container-service-mesos-marathon-ui.md).

* Obtenga información acerca de cómo demasiado[abrir firewall de hello](container-service-enable-public-access.md) ofrecen los contenedores de DC/OS tooyour de Azure tooallow acceso público.

