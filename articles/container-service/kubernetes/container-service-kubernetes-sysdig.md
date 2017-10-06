---
title: "clúster de Azure Kubernetes aaaMonitor - Sysdig | Documentos de Microsoft"
description: "Supervisión de un clúster de Kubernetes en Azure Container Service utilizando Sysdig"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a>Supervisión de un clúster de Kubernetes de Azure Container Service con Sysdig

## <a name="prerequisites"></a>Requisitos previos
En este tutorial se da por supuesto que ha [creado un clúster de Kubernetes con Azure Container Service](container-service-kubernetes-walkthrough.md).

También se da por supuesto que tiene hello azure cli y kubectl instaladas las herramientas.

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

## <a name="sysdig"></a>Sysdig
Sysdig una empresa de servicio de supervisión externa que puede supervisar los contenedores en un clúster de Kubernetes que se ejecuta en Azure. El uso de Sysdig requiere una cuenta de Sysdig activa.
Puede registrarse para obtener una cuenta en su [sitio](https://app.sysdigcloud.com).

Una vez que ha iniciado sesión en el sitio Web de toohello Sysdig en la nube, haga clic en su nombre de usuario y, en la página de hello verá la "clave de acceso". 

![Clave de API de Sysdig](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a>Instalar agentes tooKubernetes de hello Sysdig
los contenedores, Sysdig ejecuta un proceso en cada equipo utilizando un Kubernetes de toomonitor `DaemonSet`.
DaemonSets son objetos de la API de Kubernetes que ejecutan una instancia única de un contenedor por máquina.
Son perfectos para instalar herramientas como Hola a agente de supervisión de Sysdig.

tooinstall hello Sysdig daemonset, primero debe descargar [plantilla hello](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) desde sysdig. Guarde el archivo como `sysdig-daemonset.yaml`.

En Linux y OS X, puede ejecutar:

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

En PowerShell:

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

A continuación editar ese archivo tooinsert su clave de acceso, que obtiene de la cuenta Sysdig.

Por último, cree Hola DaemonSet:

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a>Visualización de la supervisión
Una vez instalado y en ejecución, agentes de hello deben bombeo tooSysdig atrás de datos.  Volver atrás toothe [sysdig panel](https://app.sysdigcloud.com) y debería ver la información acerca de los contenedores.

También puede instalara paneles específicos de Kubernetes a través del [nuevo Asistente de panel](https://app.sysdigcloud.com/#/dashboards/new).
