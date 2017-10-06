---
title: "clúster de Azure Kubernetes aaaMonitor con Datadog | Documentos de Microsoft"
description: "Supervisión de un clúster de Kubernetes en Azure Container Service utilizando Datadog"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a>Supervisión de un clúster de Azure Container Service con DataDog

## <a name="prerequisites"></a>Requisitos previos
En este tutorial se da por supuesto que ha [creado un clúster de Kubernetes con Azure Container Service](container-service-kubernetes-walkthrough.md).

También se supone que dispone de hello `az` cli de Azure y `kubectl` herramientas instaladas.

Puede probar si tiene hello `az` instalada mediante la ejecución de la herramienta:

```console
$ az --version
```

Si no tienes hello `az` herramienta instalada, se ofrecen instrucciones [aquí](https://github.com/azure/azure-cli#installation).

Puede probar si tiene hello `kubectl` instalada mediante la ejecución de la herramienta:

```console
$ kubectl version
```

Si no tiene la herramienta `kubectl` instalada, puede ejecutar:

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a>Datadog
Datadog es un servicio de supervisión que recopila datos de supervisión de los contenedores dentro del clúster del servicio de contenedor de Azure. Datadog tiene un panel de integración de Docker donde puede ver las métricas específicas dentro de los contenedores. Las métricas que se recopilan de los contenedores están organizadas por CPU, memoria, red y E/S. Datadog divide las métricas en contenedores e imágenes.

Primero debe demasiado[crear una cuenta](https://www.datadoghq.com/lpg/)

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a>Instalación de hello Datadog agente con un DaemonSet
DaemonSets usan Kubernetes toorun una sola instancia de un contenedor en cada host de clúster de Hola.
Son perfectos para ejecutar agentes de supervisión.

Una vez que ha iniciado en Datadog, puede seguir hello [Datadog instrucciones](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agentes en su clúster mediante un DaemonSet.

## <a name="conclusion"></a>Conclusión
Eso es todo. Una vez que los agentes de hello están funcionando y que ejecutan debería ver datos en la consola de hello en unos minutos. Puede visitar Hola integrado [kubernetes panel](https://app.datadoghq.com/screen/integration/kubernetes) toosee un resumen del clúster.
