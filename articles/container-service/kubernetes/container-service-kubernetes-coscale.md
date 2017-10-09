---
title: "clúster de aaaMonitor un Kubernetes de Azure con CoScale | Documentos de Microsoft"
description: "Supervisión de un clúster de Kubernetes en Azure Container Service mediante CoScale"
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a>Supervisión de un clúster de Kubernetes de Azure Container Service con CoScale

En este artículo, le mostraremos cómo hello toodeploy [CoScale](https://www.coscale.com/) toomonitor agente todos los nodos y contenedores en su Kubernetes de clúster en el servicio de contenedor de Azure. Para esta configuración se necesita una cuenta con CoScale. 


## <a name="about-coscale"></a>Acerca de CoScale 

CoScale es una plataforma de supervisión que recopila métricas y eventos de todos los contenedores de varias plataformas de orquestación. CoScale ofrece supervisión de toda la pila para los entornos de Kubernetes. Proporciona visualizaciones y análisis para todas las capas de la pila de hello: Hola SO, Kubernetes, Docker y aplicaciones que se ejecutan dentro de los contenedores. CoScale ofrece varios paneles de supervisión integrados y tiene operadores de tooallow de detección de anomalías integrados y rápida de problemas de infraestructura y las aplicaciones de toofind a los desarrolladores.

![Interfaz de usuario de CoScale](./media/container-service-kubernetes-coscale/coscale.png)

Como se muestra en este artículo, puede instalar a agentes en un toorun de clúster Kubernetes CoScale como una solución de SaaS. Si desea que tookeep los datos locales, CoScale también está disponible para la instalación local.


## <a name="prerequisites"></a>Requisitos previos

Primero debe demasiado[crear una cuenta de CoScale](https://www.coscale.com/free-trial).

En este tutorial se da por supuesto que ha [creado un clúster de Kubernetes con Azure Container Service](container-service-kubernetes-walkthrough.md).

También se supone que dispone de hello `az` CLI de Azure y `kubectl` herramientas instaladas.

Puede probar si tiene hello `az` instalada mediante la ejecución de la herramienta:

```azurecli
az --version
```

Si no tienes hello `az` herramienta instalada, se ofrecen instrucciones [aquí](/cli/azure/install-azure-cli).

Puede probar si tiene hello `kubectl` instalada mediante la ejecución de la herramienta:

```bash
kubectl version
```

Si no tiene la herramienta `kubectl` instalada, puede ejecutar:

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a>Instalación de agente de hello CoScale con un DaemonSet
[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) están utilizando Kubernetes toorun una sola instancia de un contenedor en cada host de clúster de Hola.
Son perfectos para ejecutar agentes de supervisión como el agente de CoScale Hola.

Después de iniciar sesión en tooCoScale, vaya toohello [página agente](https://app.coscale.com/) agentes de CoScale tooinstall en su clúster mediante un DaemonSet. Hola CoScale UI proporciona toocreate de pasos de configuración guiada un agente e iniciar la supervisión de su clúster Kubernetes completando.

![Configuración del agente de CoScale](./media/container-service-kubernetes-coscale/installation.png)

toostart Hola agente Hola clúster, ejecute el comando de hello proporcionado:

![Iniciar el agente de hello CoScale](./media/container-service-kubernetes-coscale/agent_script.png)

Eso es todo. Una vez que los agentes de hello están activados y ejecutándose, debería ver datos en la consola de hello en unos minutos. Visite hello [página agente](https://app.coscale.com/) toosee un resumen del clúster, lleve a cabo los pasos de configuración adicional así como paneles como hello **Kubernetes información general del clúster**.

![Información general del clúster de Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

agente de CoScale Hola se implementa automáticamente en nuevas máquinas en clúster de Hola. Hola las actualizaciones del agente automáticamente cuando se lance una nueva versión.


## <a name="next-steps"></a>Pasos siguientes

Vea hello [CoScale documentación](http://docs.coscale.com/) y [blog](https://www.coscale.com/blog) para obtener más información sobre CoScale soluciones de supervisión. 

