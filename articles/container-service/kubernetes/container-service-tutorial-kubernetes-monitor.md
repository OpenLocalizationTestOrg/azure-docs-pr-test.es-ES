---
title: tutorial de servicio de contenedor de aaaAzure - Monitor Kubernetes | Documentos de Microsoft
description: "Tutorial de Azure Container Service: supervisión de Kubernetes con Microsoft Operations Management Suite (OMS)"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Microservicios, Kubernetes, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a>Supervisión de un clúster de Kubernetes con Operations Management Suite

La supervisión de su clúster de Kubernetes y de los contenedores es fundamental, sobre todo al administrar un clúster de producción a escala con varias aplicaciones. 

Puede sacar provecho de varias soluciones de supervisión de Kubernetes, tanto de Microsoft como de otros proveedores. En este tutorial, supervisar el clúster Kubernetes mediante el uso de la solución de contenedores de hello en [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), solución de administración de TI en la nube de Microsoft. (Hola solución de contenedores de OMS está en vista previa).

Este tutorial, parte siete de siete, trata Hola siguientes tareas:

> [!div class="checklist"]
> * Obtener la configuración del área de trabajo de OMS
> * Configurar agentes OMS en nodos de hello Kubernetes
> * Obtener acceso a información de supervisión en el portal de OMS de Hola o portal de Azure

## <a name="before-you-begin"></a>Antes de empezar

En los tutoriales anteriores, una aplicación se empaqueta en imágenes del contenedor, estas imágenes cargan tooAzure del registro de contenedor y un clúster de Kubernetes creado. Si aún no ha hecho estos pasos y desearía toofollow a lo largo, devolver demasiado[Tutorial 1: crear imágenes del contenedor](./container-service-tutorial-kubernetes-prepare-app.md). 

Como mínimo, este tutorial requiere un clúster de Kubernetes con nodos de agente de Linux y una cuenta de Operations Management Suite (OMS). Si es necesario, regístrese para disfrutar de una [versión de evaluación gratuita de OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).

## <a name="get-workspace-settings"></a>Obtener la configuración del área de trabajo

Al acceder a hello [portal de OMS](https://mms.microsoft.com), vaya demasiado**configuración** > **orígenes conectados** > **servidores Linux**. Allí, puede encontrar Hola *Id. de área de trabajo* y un principal o secundario *clave de área de trabajo*. Tome nota de estos valores, que necesita tooset los agentes OMS en clúster de Hola.

## <a name="set-up-oms-agents"></a>Configuración de agentes de OMS

Este es un tooset de archivo YAML los agentes OMS en nodos de clúster de Linux Hola. Crea un recurso [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) de Kubernetes, que ejecuta un solo pod idéntico en cada nodo del clúster. Hola DaemonSet recursos es ideal para implementar a un agente de supervisión. 

Guardar Hola siguiente con el nombre el archivo de texto tooa `oms-daemonset.yaml`y reemplace los valores de marcador de posición de Hola para *myWorkspaceID* y *myWorkspaceKey* con la clave y el identificador de área de trabajo de OMS. (en producción, estos valores se pueden codificar como secretos).

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

Crear hello DaemonSet con hello siguiente comando:

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

toosee ese hello DaemonSet se crea, ejecute:

```azurecli-interactive
kubectl get daemonset
```

Salida es la siguiente de toohello similar:

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

Después de que se ejecutan los agentes de hello, tarda varios minutos para los datos de hello tooingest y proceso OMS.

## <a name="access-monitoring-data"></a>Acceso a los datos de supervisión

Ver y analizar datos con hello de supervisión de contenedores OMS de hello [soluciones de contenedor](../../log-analytics/log-analytics-containers.md) en el portal de OMS de Hola u Hola portal de Azure. 

solución de contenedor de hello tooinstall mediante hello [portal de OMS](https://mms.microsoft.com), vaya demasiado**Galería de soluciones**. A continuación, agregue **Solución de contenedor**. O bien, agregar soluciones de contenedores de Hola de hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).

En el portal de OMS de hello, busque un **contenedores** mosaico de resumen en el panel de OMS Hola. Haga clic en el icono de Hola para obtener detalles como: eventos de contenedor, errores, estado, inventario de la imagen y uso de CPU y memoria. Para obtener información más detallada, haga clic en una fila de cualquier icono o realice una [búsqueda de registros](../../log-analytics/log-analytics-log-searches.md).

![Panel de contenedores en el Portal de OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

De forma similar, en hello portal de Azure, vaya demasiado**análisis de registros** y seleccione el nombre del área de trabajo. Hola toosee **contenedores** mosaico de resumen, haga clic en **soluciones** > **contenedores**. toosee detalles, haga clic en el icono de Hola.

Vea hello [documentación de Azure Log Analytics](../../log-analytics/index.md) para obtener instrucciones detalladas para consultar y analizar los datos de supervisión.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, se ha supervisado el clúster de Kubernetes con OMS. Estas son las tareas que se han tratado:

> [!div class="checklist"]
> * Obtener la configuración del área de trabajo de OMS
> * Configurar agentes OMS en nodos de hello Kubernetes
> * Obtener acceso a información de supervisión en el portal de OMS de Hola o portal de Azure


Siga este toosee vínculo pregeneradas ejemplos de script para el servicio de contenedor.

> [!div class="nextstepaction"]
> [Ejemplos de scripts de Azure Container Service](cli-samples.md)
