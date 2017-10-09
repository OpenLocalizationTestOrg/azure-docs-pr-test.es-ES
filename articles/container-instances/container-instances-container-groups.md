---
title: aaaAzure grupos del contenedor de instancias de contenedor
description: "Descripción del funcionamiento de los Grupos de contenedores en Azure Container Instances"
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
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a>Grupos de contenedores en Azure Container Instances

recurso de nivel superior de Hello en instancias de contenedor de Azure es un grupo contenedor. Este artículo describe qué son los grupos de contenedores y qué tipos de escenarios permiten.

## <a name="how-a-container-group-works"></a>Cómo funciona un grupo de contenedores

Un grupo de contenedor es una colección de contenedores que se programan en hello mismo host de máquina y compartir un ciclo de vida, la red local y volúmenes de almacenamiento. Es similar concepto toohello de un *pod* en [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) y [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).

Hello siguiente diagrama muestra un ejemplo de un grupo contenedor que incluye varios contenedores.

![Ejemplo de grupo de contenedores][container-groups-example]

Observe lo siguiente:

- grupo de Hola se programa en una máquina de host único.
- grupo de Hello expone una única dirección IP pública, con un puerto expuesto.
- grupo de Hola se compone de dos contenedores. Un contenedor de escucha en el puerto 80, mientras Hola otro escucha en el puerto 5000.
- grupo de Hello incluye dos recursos compartidos de archivos de Azure como montajes de volumen, y cada contenedor monta uno de los recursos compartidos de hello localmente.

### <a name="networking"></a>Redes

Los grupos de contenedores comparten una dirección IP y un espacio de nombres de puerto en esa dirección IP. tooenable los clientes externos tooreach un contenedor en el grupo de hello, debe exponer el puerto de hello en dirección IP de Hola y de contenedor de Hola. Dado que los contenedores dentro de grupo de hello comparten un espacio de nombres de puerto, no se admite la asignación de puertos. Contenedores dentro de un grupo pueden llegar a entre sí a través de localhost en hello puertos que han expuesto, incluso si estos puertos no se exponen externamente en dirección IP del grupo de Hola.

### <a name="storage"></a>Storage

Puede especificar volúmenes externos toomount dentro de un grupo contenedor. Puede asignar los volúmenes en rutas de acceso específicas dentro de los contenedores individuales de hello en un grupo.

## <a name="common-scenarios"></a>Escenarios comunes

Grupos del contenedor múltiples son útiles en casos donde probablemente prefiera toodivide una sola tarea funcional en un pequeño número de imágenes de contenedor, que se pueden entregar mediante los distintos equipos y tienen requisitos de recursos independiente. Ejemplos posibles de uso serían:

- Un contenedor de aplicación y un contenedor de registro. contenedor de registro de Hello recopila registros de Hola y resultados de las métricas por aplicación principal hello y los escribe almacenamiento toolong término.
- Una aplicación y un contenedor de supervisión. Hola supervisión periódica del contenedor hace un tooensure de aplicación de toohello de solicitud que se está ejecutando y responder correctamente y genera una alerta si no lo está.
- Un contenedor para una aplicación web y un contenedor de extraer contenido más reciente de Hola de control de código fuente.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo demasiado[implementar un grupo contenedor múltiples](container-instances-multi-container-group.md) con una plantilla de Azure Resource Manager.

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png